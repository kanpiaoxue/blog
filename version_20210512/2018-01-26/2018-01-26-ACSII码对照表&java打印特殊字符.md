#ACSII码对照表&java打印特殊字符
###发表时间：2018-01-26
###分类：ASCII,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2409215" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2409215</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>得到下面的ASCII对照表的方法：在Linux上面执行命令：man ascii</p> 
 <p>&nbsp;</p> 
 <p>ASCII(7)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;Linux Programmer’s Manual&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ASCII(7)</p> 
 <p>&nbsp;</p> 
 <p>NAME</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;ascii - the ASCII character set encoded in octal, decimal, and hexadecimal</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>==============================================[start 2018-01-26 19:23]===============================================</p> 
 <p>2018-01-26 19:02，</p> 
 <p>&nbsp; &nbsp; binary 二进制的</p> 
 <p>&nbsp; &nbsp; octal 八进制的</p> 
 <p>&nbsp; &nbsp; hexadecimal 十六进制的</p> 
 <p>&nbsp; &nbsp; decimal 十进制的</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; 使用八进制（Oct）的表示方法：</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; System.out.println("hello\001world"); // hello^Aworld</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; System.out.println("hello\002world"); // hello^Bworld</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; System.out.println("hello\011world"); // hello\tworld</p> 
 <p>&nbsp;</p> 
 <p>==============================================[&nbsp; end 2018-01-26 19:23]===============================================</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>DESCRIPTION</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;ASCII is the American Standard Code for Information Interchange.&nbsp; It is a 7-bit code.&nbsp; Many 8-bit codes (such as</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;ISO 8859-1, the Linux default character set) contain ASCII as their lower half.&nbsp; The&nbsp; international&nbsp; counterpart</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;of ASCII is known as ISO 646.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;The following table contains the 128 ASCII characters.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;C program '\X' escapes are noted.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;Oct&nbsp; &nbsp;Dec&nbsp; &nbsp;Hex&nbsp; &nbsp;Char&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Oct&nbsp; &nbsp;Dec&nbsp; &nbsp;Hex&nbsp; &nbsp;Char</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;------------------------------------------------------------------------</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;000&nbsp; &nbsp;0&nbsp; &nbsp; &nbsp;00&nbsp; &nbsp; NUL '\0'&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 100&nbsp; &nbsp;64&nbsp; &nbsp; 40&nbsp; &nbsp; @</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;001&nbsp; &nbsp;1&nbsp; &nbsp; &nbsp;01&nbsp; &nbsp; SOH (start of heading)&nbsp; &nbsp; &nbsp; 101&nbsp; &nbsp;65&nbsp; &nbsp; 41&nbsp; &nbsp; A</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;002&nbsp; &nbsp;2&nbsp; &nbsp; &nbsp;02&nbsp; &nbsp; STX (start of text)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;102&nbsp; &nbsp;66&nbsp; &nbsp; 42&nbsp; &nbsp; B</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;003&nbsp; &nbsp;3&nbsp; &nbsp; &nbsp;03&nbsp; &nbsp; ETX (end of text)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;103&nbsp; &nbsp;67&nbsp; &nbsp; 43&nbsp; &nbsp; C</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;004&nbsp; &nbsp;4&nbsp; &nbsp; &nbsp;04&nbsp; &nbsp; EOT (end of transmission)&nbsp; &nbsp;104&nbsp; &nbsp;68&nbsp; &nbsp; 44&nbsp; &nbsp; D</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;005&nbsp; &nbsp;5&nbsp; &nbsp; &nbsp;05&nbsp; &nbsp; ENQ (enquiry)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;105&nbsp; &nbsp;69&nbsp; &nbsp; 45&nbsp; &nbsp; E</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;006&nbsp; &nbsp;6&nbsp; &nbsp; &nbsp;06&nbsp; &nbsp; ACK (acknowledge)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;106&nbsp; &nbsp;70&nbsp; &nbsp; 46&nbsp; &nbsp; F</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;007&nbsp; &nbsp;7&nbsp; &nbsp; &nbsp;07&nbsp; &nbsp; BEL '\a' (bell)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;107&nbsp; &nbsp;71&nbsp; &nbsp; 47&nbsp; &nbsp; G</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;010&nbsp; &nbsp;8&nbsp; &nbsp; &nbsp;08&nbsp; &nbsp; BS&nbsp; '\b' (backspace)&nbsp; &nbsp; &nbsp; &nbsp; 110&nbsp; &nbsp;72&nbsp; &nbsp; 48&nbsp; &nbsp; H</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;011&nbsp; &nbsp;9&nbsp; &nbsp; &nbsp;09&nbsp; &nbsp; HT&nbsp; '\t' (horizontal tab)&nbsp; &nbsp;111&nbsp; &nbsp;73&nbsp; &nbsp; 49&nbsp; &nbsp; I</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;012&nbsp; &nbsp;10&nbsp; &nbsp; 0A&nbsp; &nbsp; LF&nbsp; '\n' (new line)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;112&nbsp; &nbsp;74&nbsp; &nbsp; 4A&nbsp; &nbsp; J</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;013&nbsp; &nbsp;11&nbsp; &nbsp; 0B&nbsp; &nbsp; VT&nbsp; '\v' (vertical tab)&nbsp; &nbsp; &nbsp;113&nbsp; &nbsp;75&nbsp; &nbsp; 4B&nbsp; &nbsp; K</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;014&nbsp; &nbsp;12&nbsp; &nbsp; 0C&nbsp; &nbsp; FF&nbsp; '\f' (form feed)&nbsp; &nbsp; &nbsp; &nbsp; 114&nbsp; &nbsp;76&nbsp; &nbsp; 4C&nbsp; &nbsp; L</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;015&nbsp; &nbsp;13&nbsp; &nbsp; 0D&nbsp; &nbsp; CR&nbsp; '\r' (carriage ret)&nbsp; &nbsp; &nbsp;115&nbsp; &nbsp;77&nbsp; &nbsp; 4D&nbsp; &nbsp; M</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;016&nbsp; &nbsp;14&nbsp; &nbsp; 0E&nbsp; &nbsp; SO&nbsp; (shift out)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;116&nbsp; &nbsp;78&nbsp; &nbsp; 4E&nbsp; &nbsp; N</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;017&nbsp; &nbsp;15&nbsp; &nbsp; 0F&nbsp; &nbsp; SI&nbsp; (shift in)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 117&nbsp; &nbsp;79&nbsp; &nbsp; 4F&nbsp; &nbsp; O</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;020&nbsp; &nbsp;16&nbsp; &nbsp; 10&nbsp; &nbsp; DLE (data link escape)&nbsp; &nbsp; &nbsp; 120&nbsp; &nbsp;80&nbsp; &nbsp; 50&nbsp; &nbsp; P</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;021&nbsp; &nbsp;17&nbsp; &nbsp; 11&nbsp; &nbsp; DC1 (device control 1)&nbsp; &nbsp; &nbsp; 121&nbsp; &nbsp;81&nbsp; &nbsp; 51&nbsp; &nbsp; Q</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;022&nbsp; &nbsp;18&nbsp; &nbsp; 12&nbsp; &nbsp; DC2 (device control 2)&nbsp; &nbsp; &nbsp; 122&nbsp; &nbsp;82&nbsp; &nbsp; 52&nbsp; &nbsp; R</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;023&nbsp; &nbsp;19&nbsp; &nbsp; 13&nbsp; &nbsp; DC3 (device control 3)&nbsp; &nbsp; &nbsp; 123&nbsp; &nbsp;83&nbsp; &nbsp; 53&nbsp; &nbsp; S</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;024&nbsp; &nbsp;20&nbsp; &nbsp; 14&nbsp; &nbsp; DC4 (device control 4)&nbsp; &nbsp; &nbsp; 124&nbsp; &nbsp;84&nbsp; &nbsp; 54&nbsp; &nbsp; T</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;025&nbsp; &nbsp;21&nbsp; &nbsp; 15&nbsp; &nbsp; NAK (negative ack.)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;125&nbsp; &nbsp;85&nbsp; &nbsp; 55&nbsp; &nbsp; U</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;026&nbsp; &nbsp;22&nbsp; &nbsp; 16&nbsp; &nbsp; SYN (synchronous idle)&nbsp; &nbsp; &nbsp; 126&nbsp; &nbsp;86&nbsp; &nbsp; 56&nbsp; &nbsp; V</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;027&nbsp; &nbsp;23&nbsp; &nbsp; 17&nbsp; &nbsp; ETB (end of trans. blk)&nbsp; &nbsp; &nbsp;127&nbsp; &nbsp;87&nbsp; &nbsp; 57&nbsp; &nbsp; W</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;030&nbsp; &nbsp;24&nbsp; &nbsp; 18&nbsp; &nbsp; CAN (cancel)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 130&nbsp; &nbsp;88&nbsp; &nbsp; 58&nbsp; &nbsp; X</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;031&nbsp; &nbsp;25&nbsp; &nbsp; 19&nbsp; &nbsp; EM&nbsp; (end of medium)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;131&nbsp; &nbsp;89&nbsp; &nbsp; 59&nbsp; &nbsp; Y</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;032&nbsp; &nbsp;26&nbsp; &nbsp; 1A&nbsp; &nbsp; SUB (substitute)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 132&nbsp; &nbsp;90&nbsp; &nbsp; 5A&nbsp; &nbsp; Z</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;033&nbsp; &nbsp;27&nbsp; &nbsp; 1B&nbsp; &nbsp; ESC (escape)&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 133&nbsp; &nbsp;91&nbsp; &nbsp; 5B&nbsp; &nbsp; [</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;034&nbsp; &nbsp;28&nbsp; &nbsp; 1C&nbsp; &nbsp; FS&nbsp; (file separator)&nbsp; &nbsp; &nbsp; &nbsp; 134&nbsp; &nbsp;92&nbsp; &nbsp; 5C&nbsp; &nbsp; \&nbsp; '\\'</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;035&nbsp; &nbsp;29&nbsp; &nbsp; 1D&nbsp; &nbsp; GS&nbsp; (group separator)&nbsp; &nbsp; &nbsp; &nbsp;135&nbsp; &nbsp;93&nbsp; &nbsp; 5D&nbsp; &nbsp; ]</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;036&nbsp; &nbsp;30&nbsp; &nbsp; 1E&nbsp; &nbsp; RS&nbsp; (record separator)&nbsp; &nbsp; &nbsp; 136&nbsp; &nbsp;94&nbsp; &nbsp; 5E&nbsp; &nbsp; ^</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;037&nbsp; &nbsp;31&nbsp; &nbsp; 1F&nbsp; &nbsp; US&nbsp; (unit separator)&nbsp; &nbsp; &nbsp; &nbsp; 137&nbsp; &nbsp;95&nbsp; &nbsp; 5F&nbsp; &nbsp; _</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;040&nbsp; &nbsp;32&nbsp; &nbsp; 20&nbsp; &nbsp; SPACE&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;140&nbsp; &nbsp;96&nbsp; &nbsp; 60&nbsp; &nbsp; `</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;041&nbsp; &nbsp;33&nbsp; &nbsp; 21&nbsp; &nbsp; !&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;141&nbsp; &nbsp;97&nbsp; &nbsp; 61&nbsp; &nbsp; a</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;042&nbsp; &nbsp;34&nbsp; &nbsp; 22&nbsp; &nbsp; "&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;142&nbsp; &nbsp;98&nbsp; &nbsp; 62&nbsp; &nbsp; b</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;043&nbsp; &nbsp;35&nbsp; &nbsp; 23&nbsp; &nbsp; #&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;143&nbsp; &nbsp;99&nbsp; &nbsp; 63&nbsp; &nbsp; c</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;044&nbsp; &nbsp;36&nbsp; &nbsp; 24&nbsp; &nbsp; $&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;144&nbsp; &nbsp;100&nbsp; &nbsp;64&nbsp; &nbsp; d</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;045&nbsp; &nbsp;37&nbsp; &nbsp; 25&nbsp; &nbsp; %&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;145&nbsp; &nbsp;101&nbsp; &nbsp;65&nbsp; &nbsp; e</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;046&nbsp; &nbsp;38&nbsp; &nbsp; 26&nbsp; &nbsp; &amp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;146&nbsp; &nbsp;102&nbsp; &nbsp;66&nbsp; &nbsp; f</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;047&nbsp; &nbsp;39&nbsp; &nbsp; 27&nbsp; &nbsp; ´&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;147&nbsp; &nbsp;103&nbsp; &nbsp;67&nbsp; &nbsp; g</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;050&nbsp; &nbsp;40&nbsp; &nbsp; 28&nbsp; &nbsp; (&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;150&nbsp; &nbsp;104&nbsp; &nbsp;68&nbsp; &nbsp; h</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;051&nbsp; &nbsp;41&nbsp; &nbsp; 29&nbsp; &nbsp; )&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;151&nbsp; &nbsp;105&nbsp; &nbsp;69&nbsp; &nbsp; i</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;052&nbsp; &nbsp;42&nbsp; &nbsp; 2A&nbsp; &nbsp; *&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;152&nbsp; &nbsp;106&nbsp; &nbsp;6A&nbsp; &nbsp; j</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;053&nbsp; &nbsp;43&nbsp; &nbsp; 2B&nbsp; &nbsp; +&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;153&nbsp; &nbsp;107&nbsp; &nbsp;6B&nbsp; &nbsp; k</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;054&nbsp; &nbsp;44&nbsp; &nbsp; 2C&nbsp; &nbsp; ,&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;154&nbsp; &nbsp;108&nbsp; &nbsp;6C&nbsp; &nbsp; l</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;055&nbsp; &nbsp;45&nbsp; &nbsp; 2D&nbsp; &nbsp; -&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;155&nbsp; &nbsp;109&nbsp; &nbsp;6D&nbsp; &nbsp; m</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;056&nbsp; &nbsp;46&nbsp; &nbsp; 2E&nbsp; &nbsp; .&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;156&nbsp; &nbsp;110&nbsp; &nbsp;6E&nbsp; &nbsp; n</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;057&nbsp; &nbsp;47&nbsp; &nbsp; 2F&nbsp; &nbsp; /&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;157&nbsp; &nbsp;111&nbsp; &nbsp;6F&nbsp; &nbsp; o</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;060&nbsp; &nbsp;48&nbsp; &nbsp; 30&nbsp; &nbsp; 0&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;160&nbsp; &nbsp;112&nbsp; &nbsp;70&nbsp; &nbsp; p</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;061&nbsp; &nbsp;49&nbsp; &nbsp; 31&nbsp; &nbsp; 1&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;161&nbsp; &nbsp;113&nbsp; &nbsp;71&nbsp; &nbsp; q</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;062&nbsp; &nbsp;50&nbsp; &nbsp; 32&nbsp; &nbsp; 2&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;162&nbsp; &nbsp;114&nbsp; &nbsp;72&nbsp; &nbsp; r</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;063&nbsp; &nbsp;51&nbsp; &nbsp; 33&nbsp; &nbsp; 3&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;163&nbsp; &nbsp;115&nbsp; &nbsp;73&nbsp; &nbsp; s</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;064&nbsp; &nbsp;52&nbsp; &nbsp; 34&nbsp; &nbsp; 4&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;164&nbsp; &nbsp;116&nbsp; &nbsp;74&nbsp; &nbsp; t</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;065&nbsp; &nbsp;53&nbsp; &nbsp; 35&nbsp; &nbsp; 5&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;165&nbsp; &nbsp;117&nbsp; &nbsp;75&nbsp; &nbsp; u</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;066&nbsp; &nbsp;54&nbsp; &nbsp; 36&nbsp; &nbsp; 6&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;166&nbsp; &nbsp;118&nbsp; &nbsp;76&nbsp; &nbsp; v</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;067&nbsp; &nbsp;55&nbsp; &nbsp; 37&nbsp; &nbsp; 7&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;167&nbsp; &nbsp;119&nbsp; &nbsp;77&nbsp; &nbsp; w</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;070&nbsp; &nbsp;56&nbsp; &nbsp; 38&nbsp; &nbsp; 8&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;170&nbsp; &nbsp;120&nbsp; &nbsp;78&nbsp; &nbsp; x</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;071&nbsp; &nbsp;57&nbsp; &nbsp; 39&nbsp; &nbsp; 9&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;171&nbsp; &nbsp;121&nbsp; &nbsp;79&nbsp; &nbsp; y</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;072&nbsp; &nbsp;58&nbsp; &nbsp; 3A&nbsp; &nbsp; :&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;172&nbsp; &nbsp;122&nbsp; &nbsp;7A&nbsp; &nbsp; z</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;073&nbsp; &nbsp;59&nbsp; &nbsp; 3B&nbsp; &nbsp; ;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;173&nbsp; &nbsp;123&nbsp; &nbsp;7B&nbsp; &nbsp; {</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;074&nbsp; &nbsp;60&nbsp; &nbsp; 3C&nbsp; &nbsp; &lt;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;174&nbsp; &nbsp;124&nbsp; &nbsp;7C&nbsp; &nbsp; |</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;075&nbsp; &nbsp;61&nbsp; &nbsp; 3D&nbsp; &nbsp; =&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;175&nbsp; &nbsp;125&nbsp; &nbsp;7D&nbsp; &nbsp; }</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;076&nbsp; &nbsp;62&nbsp; &nbsp; 3E&nbsp; &nbsp; &gt;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;176&nbsp; &nbsp;126&nbsp; &nbsp;7E&nbsp; &nbsp; ~</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;077&nbsp; &nbsp;63&nbsp; &nbsp; 3F&nbsp; &nbsp; ?&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;177&nbsp; &nbsp;127&nbsp; &nbsp;7F&nbsp; &nbsp; DEL</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp;Tables</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;For convenience, let us give more compact tables in hex and decimal.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 2 3 4 5 6 7&nbsp; &nbsp; &nbsp; &nbsp;30 40 50 60 70 80 90 100 110 120</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; -------------&nbsp; &nbsp; &nbsp; ---------------------------------</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;0:&nbsp; &nbsp;0 @ P ` p&nbsp; &nbsp; &nbsp;0:&nbsp; &nbsp; (&nbsp; 2&nbsp; &lt;&nbsp; F&nbsp; P&nbsp; Z&nbsp; d&nbsp; &nbsp;n&nbsp; &nbsp;x</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;1: ! 1 A Q a q&nbsp; &nbsp; &nbsp;1:&nbsp; &nbsp; )&nbsp; 3&nbsp; =&nbsp; G&nbsp; Q&nbsp; [&nbsp; e&nbsp; &nbsp;o&nbsp; &nbsp;y</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;2: " 2 B R b r&nbsp; &nbsp; &nbsp;2:&nbsp; &nbsp; *&nbsp; 4&nbsp; &gt;&nbsp; H&nbsp; R&nbsp; \&nbsp; f&nbsp; &nbsp;p&nbsp; &nbsp;z</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;3: # 3 C S c s&nbsp; &nbsp; &nbsp;3: !&nbsp; +&nbsp; 5&nbsp; ?&nbsp; I&nbsp; S&nbsp; ]&nbsp; g&nbsp; &nbsp;q&nbsp; &nbsp;{</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;4: $ 4 D T d t&nbsp; &nbsp; &nbsp;4: "&nbsp; ,&nbsp; 6&nbsp; @&nbsp; J&nbsp; T&nbsp; ^&nbsp; h&nbsp; &nbsp;r&nbsp; &nbsp;|</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;5: % 5 E U e u&nbsp; &nbsp; &nbsp;5: #&nbsp; -&nbsp; 7&nbsp; A&nbsp; K&nbsp; U&nbsp; _&nbsp; i&nbsp; &nbsp;s&nbsp; &nbsp;}</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;6: &amp; 6 F V f v&nbsp; &nbsp; &nbsp;6: $&nbsp; .&nbsp; 8&nbsp; B&nbsp; L&nbsp; V&nbsp; `&nbsp; j&nbsp; &nbsp;t&nbsp; &nbsp;~</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;7: ´ 7 G W g w&nbsp; &nbsp; &nbsp;7: %&nbsp; /&nbsp; 9&nbsp; C&nbsp; M&nbsp; W&nbsp; a&nbsp; k&nbsp; &nbsp;u&nbsp; DEL</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;8: ( 8 H X h x&nbsp; &nbsp; &nbsp;8: &amp;&nbsp; 0&nbsp; :&nbsp; D&nbsp; N&nbsp; X&nbsp; b&nbsp; l&nbsp; &nbsp;v</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;9: ) 9 I Y i y&nbsp; &nbsp; &nbsp;9: ´&nbsp; 1&nbsp; ;&nbsp; E&nbsp; O&nbsp; Y&nbsp; c&nbsp; m&nbsp; &nbsp;w</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;A: * : J Z j z</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;B: + ; K [ k {</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;C: , &lt; L \ l |</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;D: - = M ] m }</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;E: . &gt; N ^ n ~</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;F: / ? O _ o DEL</p> 
 <p>&nbsp;</p> 
 <p>NOTES</p> 
 <p>&nbsp; &nbsp;History</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;An ascii manual page appeared in Version 7 of AT&amp;T UNIX.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;On&nbsp; older&nbsp; terminals, the underscore code is displayed as a left arrow, called backarrow, the caret is displayed</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;as an up-arrow and the vertical bar has a hole in the middle.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;Uppercase and lowercase characters differ by just one bit and the ASCII character&nbsp; 2&nbsp; differs&nbsp; from&nbsp; the&nbsp; double</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;quote&nbsp; by just one bit, too.&nbsp; That made it much easier to encode characters mechanically or with a non-microcon-</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;troller-based electronic keyboard and that pairing was found on old teletypes.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;The ASCII standard was published by the United States of America Standards Institute (USASI) in 1968.</p> 
 <p>&nbsp;</p> 
 <p>SEE ALSO</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;iso_8859-1(7), iso_8859-10(7), iso_8859-13(7), iso_8859-14(7),&nbsp; iso_8859-15(7),&nbsp; iso_8859-16(7),&nbsp; iso_8859-2(7),</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;iso_8859-3(7), iso_8859-4(7), iso_8859-5(7), iso_8859-6(7), iso_8859-7(7), iso_8859-8(7), iso_8859-9(7)</p> 
 <p>&nbsp;</p> 
 <p>COLOPHON</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;This page is part of release 3.22 of the Linux man-pages project.&nbsp; A description of the project, and information</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp;about reporting bugs, can be found at http://www.kernel.org/doc/man-pages/.</p> 
 <p>&nbsp;</p> 
 <p>Linux&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;2009-02-12&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ASCII(7)</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>==============================================[start 2018-01-26 19:35]===============================================</p> 
 <p>&nbsp; &nbsp; static void test1() throws IOException {</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; StringBuilder builder = new StringBuilder();</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; builder</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("000:").append("\000").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("001:").append("\001").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("002:").append("\002").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("003:").append("\003").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("004:").append("\004").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("005:").append("\005").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("006:").append("\006").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("007:").append("\007").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("010:").append("\010").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("011:").append("\011").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("012:").append("\012").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("013:").append("\013").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("014:").append("\014").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("015:").append("\015").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("016:").append("\016").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("017:").append("\017").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("020:").append("\020").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("021:").append("\021").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("022:").append("\022").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("023:").append("\023").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("024:").append("\024").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("025:").append("\025").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("026:").append("\026").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("027:").append("\027").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("030:").append("\030").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("031:").append("\031").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("032:").append("\032").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("033:").append("\033").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("034:").append("\034").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("035:").append("\035").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("036:").append("\036").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("037:").append("\037").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("040:").append("\040").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("041:").append("\041").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("042:").append("\042").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("043:").append("\043").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("044:").append("\044").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("045:").append("\045").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("046:").append("\046").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("047:").append("\047").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("050:").append("\050").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("051:").append("\051").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("052:").append("\052").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("053:").append("\053").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("054:").append("\054").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("055:").append("\055").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("056:").append("\056").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("057:").append("\057").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("060:").append("\060").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("061:").append("\061").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("062:").append("\062").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("063:").append("\063").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("064:").append("\064").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("065:").append("\065").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("066:").append("\066").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("067:").append("\067").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("070:").append("\070").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("071:").append("\071").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("072:").append("\072").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("073:").append("\073").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("074:").append("\074").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("075:").append("\075").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("076:").append("\076").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("077:").append("\077").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("100:").append("\100").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("101:").append("\101").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("102:").append("\102").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("103:").append("\103").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("104:").append("\104").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("105:").append("\105").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("106:").append("\106").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("107:").append("\107").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("110:").append("\110").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("111:").append("\111").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("112:").append("\112").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("113:").append("\113").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("114:").append("\114").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("115:").append("\115").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("116:").append("\116").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("117:").append("\117").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("120:").append("\120").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("121:").append("\121").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("122:").append("\122").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("123:").append("\123").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("124:").append("\124").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("125:").append("\125").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("126:").append("\126").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("127:").append("\127").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("130:").append("\130").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("131:").append("\131").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("132:").append("\132").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("133:").append("\133").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("134:").append("\134").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("135:").append("\135").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("136:").append("\136").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("137:").append("\137").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("140:").append("\140").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("141:").append("\141").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("142:").append("\142").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("143:").append("\143").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("144:").append("\144").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("145:").append("\145").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("146:").append("\146").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("147:").append("\147").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("150:").append("\150").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("151:").append("\151").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("152:").append("\152").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("153:").append("\153").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("154:").append("\154").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("155:").append("\155").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("156:").append("\156").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("157:").append("\157").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("160:").append("\160").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("161:").append("\161").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("162:").append("\162").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("163:").append("\163").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("164:").append("\164").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("165:").append("\165").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("166:").append("\166").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("167:").append("\167").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("170:").append("\170").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("171:").append("\171").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("172:").append("\172").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("173:").append("\173").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("174:").append("\174").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("175:").append("\175").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("176:").append("\176").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; .append("177:").append("\177").append("\n")</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; ;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; String msg = builder.toString();</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; System.out.println(msg);</p> 
 <p>&nbsp;</p> 
 <p>&nbsp; &nbsp; &nbsp; &nbsp; Files.write(msg.getBytes(), new File("/Users/kanpiaoxue/tmp/20180126193115.txt"));</p> 
 <p>&nbsp; &nbsp; }</p> 
 <p>&nbsp;</p> 
 <p>000:^@</p> 
 <p>001:^A</p> 
 <p>002:^B</p> 
 <p>003:^C</p> 
 <p>004:^D</p> 
 <p>005:^E</p> 
 <p>006:^F</p> 
 <p>007:^G</p> 
 <p>010</p> 
 <p>011:</p> 
 <p>012:</p> 
 <p>&nbsp;</p> 
 <p>013:^K</p> 
 <p>014:^L</p> 
 <p>015:</p> 
 <p>016:^N</p> 
 <p>017:^O</p> 
 <p>020:^P</p> 
 <p>021:^Q</p> 
 <p>022:^R</p> 
 <p>023:^S</p> 
 <p>024:^T</p> 
 <p>025:^U</p> 
 <p>026:^V</p> 
 <p>027:^W</p> 
 <p>030:^X</p> 
 <p>031:^Y</p> 
 <p>032:^Z</p> 
 <p>033:ESC</p> 
 <p>034:^\</p> 
 <p>035:^]</p> 
 <p>036:^^</p> 
 <p>037:^_</p> 
 <p>040:</p> 
 <p>041:!</p> 
 <p>042:"</p> 
 <p>043:#</p> 
 <p>044:$</p> 
 <p>045:%</p> 
 <p>046:&amp;</p> 
 <p>047:'</p> 
 <p>050:(</p> 
 <p>051:)</p> 
 <p>052:*</p> 
 <p>053:+</p> 
 <p>054:,</p> 
 <p>055:-</p> 
 <p>056:.</p> 
 <p>057:/</p> 
 <p>060:0</p> 
 <p>061:1</p> 
 <p>062:2</p> 
 <p>063:3</p> 
 <p>064:4</p> 
 <p>065:5</p> 
 <p>066:6</p> 
 <p>067:7</p> 
 <p>070:8</p> 
 <p>071:9</p> 
 <p>072::</p> 
 <p>073:;</p> 
 <p>074:&lt;</p> 
 <p>075:=</p> 
 <p>076:&gt;</p> 
 <p>077:?</p> 
 <p>100:@</p> 
 <p>101:A</p> 
 <p>102:B</p> 
 <p>103:C</p> 
 <p>104:D</p> 
 <p>105:E</p> 
 <p>106:F</p> 
 <p>107:G</p> 
 <p>110:H</p> 
 <p>111:I</p> 
 <p>112:J</p> 
 <p>113:K</p> 
 <p>114:L</p> 
 <p>115:M</p> 
 <p>116:N</p> 
 <p>117:O</p> 
 <p>120:P</p> 
 <p>121:Q</p> 
 <p>122:R</p> 
 <p>123:S</p> 
 <p>124:T</p> 
 <p>125:U</p> 
 <p>126:V</p> 
 <p>127:W</p> 
 <p>130:X</p> 
 <p>131:Y</p> 
 <p>132:Z</p> 
 <p>133:[</p> 
 <p>134:\</p> 
 <p>135:]</p> 
 <p>136:^</p> 
 <p>137:_</p> 
 <p>140:`</p> 
 <p>141:a</p> 
 <p>142:b</p> 
 <p>143:c</p> 
 <p>144:d</p> 
 <p>145:e</p> 
 <p>146:f</p> 
 <p>147:g</p> 
 <p>150:h</p> 
 <p>151:i</p> 
 <p>152:j</p> 
 <p>153:k</p> 
 <p>154:l</p> 
 <p>155:m</p> 
 <p>156:n</p> 
 <p>157:o</p> 
 <p>160:p</p> 
 <p>161:q</p> 
 <p>162:r</p> 
 <p>163:s</p> 
 <p>164:t</p> 
 <p>165:u</p> 
 <p>166:v</p> 
 <p>167:w</p> 
 <p>170:x</p> 
 <p>171:y</p> 
 <p>172:z</p> 
 <p>173:{</p> 
 <p>174:|</p> 
 <p>175:}</p> 
 <p>176:~</p> 
 <p>177:^?</p> 
 <p>==============================================[&nbsp; end 2018-01-26 19:35]===============================================</p> 
 <p>&nbsp;</p> 
</div>