#生成Excel / 读取Excel
###发表时间：2013-12-23
###分类：POI,java,excel
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1993817" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1993817</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我们常常需要在web中导出excel。</p> 
 <p>这里给出一个方法，采用poi的框架，生成excel。用response打出到web页面。</p> 
 <pre name="code" class="java">	/**
	 * &lt;pre&gt;
	 * 导出excel工具方法
	 * 
	 * @author kanpiaoxue 
	 * date 2011-09-02
	 * @param response
	 * @param datas
	 *            数据
	 * @param sheetName
	 *            sheet的名字
	 * 
	 *            [备注] 默认带有excel导出的名字。就是当日的日期和时间的组合：2011-09-02_08_37_35.xls
	 * 需要 org.apache.poi 的jar包
	 × google的 guava.jar
	 * &lt;/pre&gt;
	 */
	public static void exportExcelUtil(HttpServletResponse response,
			List&lt;List&lt;String&gt;&gt; datas, String sheetName) {

		checkNotNull(response);
		checkNotNull(datas);
		checkArgument(!StringUtils.isEmpty(sheetName),
				"sheetName is empty or null!");

		class ExcelTool {
			public HSSFCellStyle getTitleStyle(HSSFWorkbook wb) {
				HSSFCellStyle style = wb.createCellStyle();
				style.setAlignment(HSSFCellStyle.ALIGN_CENTER);// 标题居中对齐
				style.setVerticalAlignment(HSSFCellStyle.VERTICAL_CENTER);
				style.setFillPattern(HSSFCellStyle.SOLID_FOREGROUND);
				style.setFillForegroundColor(HSSFColor.PALE_BLUE.index);
				style.setBorderTop(HSSFCellStyle.BORDER_THIN);
				style.setBorderBottom(HSSFCellStyle.BORDER_THIN);
				style.setBorderLeft(HSSFCellStyle.BORDER_THIN);
				style.setBorderRight(HSSFCellStyle.BORDER_THIN);
				style.setWrapText(true);
				return style;
			}

			private HSSFCellStyle getStringStyle(HSSFWorkbook wb) {
				// create cell style
				HSSFCellStyle style = wb.createCellStyle();
				// set the style of cell
				style.setAlignment(HSSFCellStyle.ALIGN_RIGHT);// 数据右对齐
				style.setVerticalAlignment(HSSFCellStyle.VERTICAL_CENTER);
				style.setBorderTop(HSSFCellStyle.BORDER_THIN);
				style.setBorderBottom(HSSFCellStyle.BORDER_THIN);
				style.setBorderLeft(HSSFCellStyle.BORDER_THIN);
				style.setBorderRight(HSSFCellStyle.BORDER_THIN);
				style.setWrapText(true);
				return style;
			}
		}

		ExcelTool excelTool = new ExcelTool();
		// create the excel work book
		HSSFWorkbook wb = new HSSFWorkbook();
		// create the sheet
		HSSFSheet sheet = wb.createSheet(sheetName);

		// get the style of title cell
		HSSFCellStyle titleStyle = excelTool.getTitleStyle(wb);
		HSSFCellStyle dataStyle = excelTool.getStringStyle(wb);

		int i = 0;
		for (List&lt;String&gt; innerList : datas) {
			HSSFCellStyle tmpStyle = dataStyle;
			HSSFRow row = sheet.createRow(i);
			if (i == 0) {// table header
				row.setHeight((short) 500);
				tmpStyle = titleStyle;
			}
			int j = 0;
			for (String str : innerList) {
				HSSFCell cell = row.createCell(j);
				cell.setCellStyle(tmpStyle);
				cell.setCellValue(new HSSFRichTextString(str));
				sheet.setColumnWidth(j, 6000);
				j++;
			}
			i++;
		}

		response.reset();
		response.setContentType("application/vnd.ms-excel; charset=utf8");
		response.setHeader("Content-Disposition",
				"attachment; filename="
						+ XPDateUtils.formatDateSecondLongPattern(new Date())
								.replaceAll("-", "_").replaceAll(":", "_")
								.replaceAll(" ", "_") + ".xls");
		OutputStream out = null;
		try {
			out = response.getOutputStream();
			wb.write(out);
		} catch (IOException e) {
			LOGGER.error("Exception: download excel " + e.getMessage(), e);
		} finally {
			IOUtils.closeQuietly(out);
		}
	}</pre> 
 <p>&nbsp;为了日常使用，我把web导出Excel稍微的改装了一下，形成本地File文件的excel导出。</p> 
 <pre name="code" class="java">package org.kanpiaoxue.staticClass;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.nio.charset.Charset;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.List;

import org.apache.commons.collections.CollectionUtils;
import org.apache.commons.lang.StringUtils;
import org.apache.log4j.Logger;
import org.apache.poi.hssf.usermodel.HSSFCell;
import org.apache.poi.hssf.usermodel.HSSFCellStyle;
import org.apache.poi.hssf.usermodel.HSSFRichTextString;
import org.apache.poi.hssf.usermodel.HSSFRow;
import org.apache.poi.hssf.usermodel.HSSFSheet;
import org.apache.poi.hssf.usermodel.HSSFWorkbook;
import org.apache.poi.hssf.util.HSSFColor;
import org.apache.poi.util.IOUtils;

import com.google.common.base.Preconditions;
import com.google.common.base.Splitter;
import com.google.common.collect.Lists;
import com.google.common.io.Files;

public class ExportExcell {
	private static final Logger LOGGER = Logger.getLogger(ExportExcell.class);

	public static void main(String[] args) throws Exception {
		testStaticClass();
	}

	public static void testStaticClass() throws Exception {
		String dir = System.getProperty("user.dir")
				+ "/src/org/kanpiaoxue/staticClass/file" + File.separator;
		String inputFileName = dir + "编辑1.txt";
		String outputFileName = dir + "export.xls";
		System.out.println(dir);
		File file = new File(inputFileName);
		List&lt;String&gt; lines = Files.readLines(file, Charset.forName("utf-8"));
		List&lt;List&lt;String&gt;&gt; rs = Lists.newArrayList();
		for (String line : lines) {
			List&lt;String&gt; lst = Splitter.on(' ').omitEmptyStrings()
					.trimResults().splitToList(line);
			if (CollectionUtils.isEmpty(lst)) {
				continue;
			}
			System.out.println(lst);
			rs.add(lst);
		}

		exportExcelUtil(new FileOutputStream(new File(outputFileName)), rs,
				"hello");
	}

	/**
	 * &lt;pre&gt;
	 * 导出excel工具方法
	 * 
	 * @author kanpiaoxue 
	 * date 2011-09-02
	 * @param response
	 * @param datas
	 *            数据
	 * @param sheetName
	 *            sheet的名字
	 * 
	 *            [备注] 默认带有excel导出的名字。就是当日的日期和时间的组合：2011-09-02_08_37_35.xls
	 * 需要 org.apache.poi 的jar包
	 * 	 × google的 guava.jar
	 * &lt;/pre&gt;
	 */
	public static void exportExcelUtil(OutputStream fileOutputStream,
			List&lt;List&lt;String&gt;&gt; datas, String sheetName) {

		Preconditions.checkNotNull(fileOutputStream);
		Preconditions.checkNotNull(datas);
		Preconditions.checkArgument(!StringUtils.isEmpty(sheetName),
				"sheetName is empty or null!");

		class ExcelTool {
			public HSSFCellStyle getTitleStyle(HSSFWorkbook wb) {
				HSSFCellStyle style = wb.createCellStyle();
				style.setAlignment(HSSFCellStyle.ALIGN_CENTER);// 标题居中对齐
				style.setVerticalAlignment(HSSFCellStyle.VERTICAL_CENTER);
				style.setFillPattern(HSSFCellStyle.SOLID_FOREGROUND);
				style.setFillForegroundColor(HSSFColor.PALE_BLUE.index);
				style.setBorderTop(HSSFCellStyle.BORDER_THIN);
				style.setBorderBottom(HSSFCellStyle.BORDER_THIN);
				style.setBorderLeft(HSSFCellStyle.BORDER_THIN);
				style.setBorderRight(HSSFCellStyle.BORDER_THIN);
				style.setWrapText(true);
				return style;
			}

			private HSSFCellStyle getStringStyle(HSSFWorkbook wb) {
				// create cell style
				HSSFCellStyle style = wb.createCellStyle();
				// set the style of cell
				style.setAlignment(HSSFCellStyle.ALIGN_RIGHT);// 数据右对齐
				style.setVerticalAlignment(HSSFCellStyle.VERTICAL_CENTER);
				style.setBorderTop(HSSFCellStyle.BORDER_THIN);
				style.setBorderBottom(HSSFCellStyle.BORDER_THIN);
				style.setBorderLeft(HSSFCellStyle.BORDER_THIN);
				style.setBorderRight(HSSFCellStyle.BORDER_THIN);
				style.setWrapText(true);
				return style;
			}
		}

		ExcelTool excelTool = new ExcelTool();
		// create the excel work book
		HSSFWorkbook wb = new HSSFWorkbook();
		// create the sheet
		HSSFSheet sheet = wb.createSheet(sheetName);

		// get the style of title cell
		HSSFCellStyle titleStyle = excelTool.getTitleStyle(wb);
		HSSFCellStyle dataStyle = excelTool.getStringStyle(wb);

		int i = 0;
		for (List&lt;String&gt; innerList : datas) {
			HSSFCellStyle tmpStyle = dataStyle;
			HSSFRow row = sheet.createRow(i);
			if (i == 0) {// table header
				row.setHeight((short) 500);
				tmpStyle = titleStyle;
			}
			int j = 0;
			for (String str : innerList) {
				HSSFCell cell = row.createCell(j);
				cell.setCellStyle(tmpStyle);
				cell.setCellValue(new HSSFRichTextString(str));
				sheet.setColumnWidth(j, 6000);
				j++;
			}
			i++;
		}

		try {
			wb.write(fileOutputStream);
		} catch (IOException e) {
			LOGGER.error("Exception: download excel " + e.getMessage(), e);
		} finally {
			IOUtils.closeQuietly(fileOutputStream);
		}
	}

	public static String formatDateSecondLongPattern(Date date) {
		SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		return format.format(date);
	}

}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;读取Excel</p> 
 <pre name="code" class="java">	/**
	 * &lt;pre&gt;
	 * @param fileName
	 * @return 读取Excel的内容
	 * &lt;/pre&gt;
	 */
	public static List&lt;List&lt;String&gt;&gt; readExcel(String fileName)
			throws Exception {
		// EXCEL_SUFFIX
		checkArgument(!Strings.isNullOrEmpty(fileName),
				"fileName is null or empty!");
		fileName = fileName.trim();
		checkArgument(fileName.endsWith(EXCEL_SUFFIX), "fileName not endsWith "
				+ EXCEL_SUFFIX);

		InputStream inputStream = new FileInputStream(new File(fileName));

		return readExcel(inputStream);
	}

	/**
	 * &lt;pre&gt;
	 * @param fileName
	 * @return 读取Excel的内容
	 * &lt;/pre&gt;
	 */
	public static List&lt;List&lt;String&gt;&gt; readExcel(InputStream inputStream)
			throws Exception {

		List&lt;List&lt;String&gt;&gt; rsList = newArrayList();
		try {

			POIFSFileSystem fs = new POIFSFileSystem(inputStream);
			HSSFWorkbook wb = new HSSFWorkbook(fs);

			HSSFSheet sheet = wb.getSheetAt(0);
			// 得到总行数
			int rowNum = sheet.getLastRowNum();
			for (int i = 0; i &lt;= rowNum; i++) {
				List&lt;String&gt; rowDatas = newArrayList();
				HSSFRow row = sheet.getRow(i);
				int colNum = row.getPhysicalNumberOfCells();
				for (int j = 0; j &lt; colNum; j++) {
					rowDatas.add(getCellFormatValue(row.getCell(j)));
				}
				rsList.add(rowDatas);
			}
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			IOUtils.closeQuietly(inputStream);
		}
		return rsList;
	}

	/**
	 * 根据HSSFCell类型设置数据
	 * 
	 * @param cell
	 * @return
	 */
	private static String getCellFormatValue(HSSFCell cell) {
		String cellvalue = "";
		if (cell != null) {
			// 判断当前Cell的Type
			switch (cell.getCellType()) {
			// 如果当前Cell的Type为NUMERIC
			case HSSFCell.CELL_TYPE_NUMERIC:
			case HSSFCell.CELL_TYPE_FORMULA: {
				// 判断当前的cell是否为Date
				if (HSSFDateUtil.isCellDateFormatted(cell)) {
					// 如果是Date类型则，转化为Data格式
					Date date = cell.getDateCellValue();
					cellvalue = XPDateUtils.formatDateSecondLongPattern(date);

				}
				// 如果是纯数字
				else {
					// 取得当前Cell的数值
					cellvalue = String.valueOf(cell.getNumericCellValue());
				}
				break;
			}
			// 如果当前Cell的Type为String
			case HSSFCell.CELL_TYPE_STRING:
				// 取得当前的Cell字符串
				cellvalue = cell.getRichStringCellValue().getString();
				break;
			// 默认的Cell值
			default:
				cellvalue = "";
			}
		}
		return cellvalue;

	}</pre> 
 <p>&nbsp;</p> 
</div>