#javascript分隔array(How to split an array into chunks of the same size)
###发表时间：2018-12-14
###分类：javascript,经验,array
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2435216" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2435216</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;《How to split an array into chunks of the same size easily in Javascript》</p> 
 <p><a href="https://ourcodeworld.com/articles/read/278/how-to-split-an-array-into-chunks-of-the-same-size-easily-in-javascript">https://ourcodeworld.com/articles/read/278/how-to-split-an-array-into-chunks-of-the-same-size-easily-in-javascript</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">/**
 * Returns an array with arrays of the given size.
 *
 * @param myArray {Array} Array to split
 * @param chunkSize {Integer} Size of every group
 */
function chunkArray(myArray, chunk_size){
    var results = [];

    while (myArray.length) {
        results.push(myArray.splice(0, chunk_size));
    }

    return results;
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p>In this article, you'll learn to split a Javascript array into chunks with a specified size using different implementations.</p> 
 <h3>1. Using a for loop and the slice function</h3> 
 <p>Basically, every method will use the slice method in order to split the array, in this case what makes this method different is the for loop.</p> 
 <p>In case that the array is not uniform, the remaining items will be in an array too, however the size will be less for obvious reasons.</p> 
 <pre name="code" class="java">/**
 * Returns an array with arrays of the given size.
 *
 * @param myArray {Array} array to split
 * @param chunk_size {Integer} Size of every group
 */
function chunkArray(myArray, chunk_size){
    var index = 0;
    var arrayLength = myArray.length;
    var tempArray = [];
    
    for (index = 0; index &lt; arrayLength; index += chunk_size) {
        myChunk = myArray.slice(index, index+chunk_size);
        // Do something if you want with the group
        tempArray.push(myChunk);
    }

    return tempArray;
}
// Split in group of 3 items
var result = chunkArray([1,2,3,4,5,6,7,8], 3);
// Outputs : [ [1,2,3] , [4,5,6] ,[7,8] ]
console.log(result);</pre> 
 <p>&nbsp;</p> 
 <h3>2. Using a for loop, slice and set&nbsp;function in the prototype of array</h3> 
 <p>You can register custom functions in the prototype of a function, in this case you can create a custom function with the name chunk that accomplishes our goal:</p> 
 <pre name="code" class="java">/**
 * Define the chunk method in the prototype of an array
 * that returns an array with arrays of the given size.
 *
 * @param chunkSize {Integer} Size of every group
 */
Object.defineProperty(Array.prototype, 'chunk', {
    value: function(chunkSize){
        var temporal = [];
        
        for (var i = 0; i &lt; this.length; i+= chunkSize){
            temporal.push(this.slice(i,i+chunkSize));
        }
                
        return temporal;
    }
});
// Split in group of 3 items
var result = [1,2,3,4,5,6,7,8].chunk(3);
// Outputs : [ [1,2,3] , [4,5,6] ,[7,8] ]
console.log(result);</pre> 
 <p>&nbsp;</p> 
 <p>As you can see,&nbsp;the principle is the same using a for loop and the slice function but instead of use it in a function, is registered in the prototype of the array.</p> 
 <h3>3. Using array map in the prototype of array</h3> 
 <p>The&nbsp;<code style="font-size: 16.2px; padding: 2px 4px; font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; color: #03a9f4; background-color: #f7f7f7; border-radius: 2px;">map</code>&nbsp;function calls a provided callback function once for each element in an array, in order, and constructs a new array from the results. The function will return an array with a length defined by the division of the length of the providen array by the size of the chunk. The fill function (as no parameter providen) will fill the created array with undefined and finally every undefined value in the array will be replaced by a new array (the result of slice the providen array with the proper index).</p> 
 <pre name="code" class="java">/**
 * Define the chunk method in the prototype of an array
 * that returns an array with arrays of the given size.
 *
 * @param chunkSize {Integer} Size of every group
 */
Object.defineProperty(Array.prototype, 'chunk', {
    value: function(chunkSize) {
        var that = this;
        return Array(Math.ceil(that.length/chunkSize)).fill().map(function(_,i){
            return that.slice(i*chunkSize,i*chunkSize+chunkSize);
        });
    }
});

// Split in group of 3 items
var result = [1,2,3,4,5,6,7,8].chunk(3);
// Outputs : [ [1,2,3] , [4,5,6] ,[7,8] ]
console.log(result);</pre> 
 <p>&nbsp;</p> 
 <h3>4. Using a while loop and slice</h3> 
 <p>In tipical and normal conditions&nbsp;the while loop&nbsp;is slightly faster. However we should be aware that these performance gains are significant for large number of iterations. Therefore, if your array is huge and you want to split in chunks with a low number, you should consider in use the method that uses while to drastically increase the performance.</p> 
 <pre name="code" class="java">/**
 * Returns an array with arrays of the given size.
 *
 * @param myArray {Array} Array to split
 * @param chunkSize {Integer} Size of every group
 */
function chunkArray(myArray, chunk_size){
    var results = [];
    
    while (myArray.length) {
        results.push(myArray.splice(0, chunk_size));
    }
    
    return results;
}

// Split in group of 3 items
var result = chunkArray([1,2,3,4,5,6,7,8], 3);
// Outputs : [ [1,2,3] , [4,5,6] ,[7,8] ]
console.log(result);</pre> 
 <p>&nbsp;</p> 
 <h3>5. Using slice and concat within a recursive function</h3> 
 <p>In this method the&nbsp;recursion is fairly expensive if we talk about performance and browser resources. Besides,&nbsp;<code style="font-size: 16.2px; padding: 2px 4px; font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; color: #03a9f4; background-color: #f7f7f7; border-radius: 2px;">concat</code>&nbsp;function is in some browsers significantly slower than the&nbsp;<code style="font-size: 16.2px; padding: 2px 4px; font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; color: #03a9f4; background-color: #f7f7f7; border-radius: 2px;">join</code>&nbsp;method.</p> 
 <pre name="code" class="java">/**
 * Define the chunk method in the prototype of an array
 * that returns an array with arrays of the given size (with a recursive function).
 *
 * @param chunk_size {Integer} Size of every group
 */
Array.prototype.chunk = function (chunk_size) {
    if ( !this.length ) {
        return [];
    }

    return [ this.slice( 0, chunk_size ) ].concat(this.slice(chunk_size).chunk(chunk_size));
};</pre> 
 <p>&nbsp;</p> 
 <p><span style="font-weight: bold;">Disclaimer: don't use in production environments with huge amount of data.</span></p> 
 <h2>About performance</h2> 
 <p>Our simple benchmark will be to split an array of 100000 (100K) items (only numbers) into chunks of 3 items/array. This task will be executed 1000 (1K) times in order to provide high accuracy, the values are given in milliseconds.</p> 
 <p>The benchmark has been executed in a machine with the following specifications:</p> 
 <ul> 
  <li>Operative system Windows 10 Pro 64-bit</li> 
  <li>Chrome&nbsp;53.0.2785.116 m (64-bit)</li> 
  <li>Intel(R) Core(TM) i5-4590 CPU @ 3.30GHz (4 CPUs), ~3.3GHz</li> 
  <li>8192MB RAM</li> 
 </ul> 
 <div class="table-responsive"> 
  <table class="table table-hover" style="border-collapse: collapse; border-spacing: 0px; background-color: transparent; width: 1129px; max-width: 100%; margin-bottom: 29px;">
   <tbody> 
    <tr> 
     <th style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">Method</th> 
     <th style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">Total time (ms)</th> 
     <th style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">Average time per task (ms)</th> 
    </tr> 
    <tr style="background-color: #f5f5f5;"> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">1 (for loop)</td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">5778.015000000001</td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">5.776805000000013</td> 
    </tr> 
    <tr> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">2 (for loop in prototype)</td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">5681.145</td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">5.679875000000007</td> 
    </tr> 
    <tr> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">3 (array map in prototype)</td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;"><span style="color: #ff9900;">8855.470000000001</span></td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;"><span style="color: #ff9900;">8.854190000000001</span></td> 
    </tr> 
    <tr> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">4 (while loop)</td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;"><span style="color: #339966;">1468.6650000000002</span></td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;"><span style="color: #339966;">1.468275000000002</span></td> 
    </tr> 
    <tr> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;">5 (recursive function with slice and concat)</td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;"><span style="color: #ff0000;">TEST-CRASHES</span></td> 
     <td style="padding: 8px 12px; line-height: 1.618; vertical-align: top; border-top: 1px solid #f0f0f0;"><span style="color: #ff0000;">TEST-CRASHES</span></td> 
    </tr> 
   </tbody>
  </table> 
 </div> 
 <ul> 
  <li>The while loop seems to be the quickest way to split an array into chunks with a high performance in comparison to others.</li> 
  <li>A detail to notice in the benchmark, is that the bigger the number of items in every chunk, the quicker the task is executed.</li> 
  <li>With the method number 5, the browser crashes so the usage of this method is discouraged for huge amount of data.</li> 
 </ul> 
 <p>Have fun&nbsp;!</p> 
</div>