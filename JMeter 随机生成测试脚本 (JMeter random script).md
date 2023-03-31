Q: jmeter 编写一个随机生成A、B 、C、D的脚本

---

A: 要编写一个在 JMeter 中随机生成 A、B、C、D 的脚本，可以使用以下步骤：

1.  添加一个 Thread Group，指定用户数、循环次数等基本信息。
2.  添加一个 HTTP Request，默认请求地址为 [http://example.com。](http://example.com%E3%80%82)
3.  在 HTTP Request 中添加一个随机变量 Random Variable，名称为 letter，设定取值范围为 A|B|C|D。
4.  在 HTTP Request 中的 Path、Parameters、Body 中使用 ${letter} 引用随机变量。
5.  运行测试，JMeter 会在每个线程中随机生成 A、B、C、D 中的一个，发送到 [http://example.com。](http://example.com%E3%80%82)

具体实现步骤如下：

1.  打开 JMeter，创建一个新的测试计划。
2.  右键单击测试计划，选择添加 -> Threads(Users) -> Thread Group。
3.  在线程组的属性中，设置线程数和循环次数等基本信息。比如，可以设置线程数为 10，循环次数为 5。
4.  右键单击线程组，选择添加 -> Sampler -> HTTP Request。
5.  在 HTTP Request 的属性中，设置请求地址为 [http://example.com。](http://example.com%E3%80%82)
6.  在 HTTP Request 中，点击添加 -> Config Element -> Random Variable。
7.  在 Random Variable 的属性中，设置变量名称为 letter，设定取值范围为 A|B|C|D。
8.  在 HTTP Request 中的 Path、Parameters、Body 中，使用 ${letter} 引用随机变量。比如，可以将 Path 设定为 /${letter}。
9.  保存测试计划，点击运行按钮开始测试。

执行测试后，JMeter 会在每个线程中随机生成 A、B、C、D 中的一个，发送到 [http://example.com。可以通过查看测试结果，确认请求是否正确发送。](http://example.com%E3%80%82%E5%8F%AF%E4%BB%A5%E9%80%9A%E8%BF%87%E6%9F%A5%E7%9C%8B%E6%B5%8B%E8%AF%95%E7%BB%93%E6%9E%9C%EF%BC%8C%E7%A1%AE%E8%AE%A4%E8%AF%B7%E6%B1%82%E6%98%AF%E5%90%A6%E6%AD%A3%E7%A1%AE%E5%8F%91%E9%80%81%E3%80%82)

---

Q: Random Variable怎么配置

---

A: 在 JMeter 中，Random Variable 是一种 Config Element，可以用来生成随机数或字符串，并将其保存为一个 JMeter 变量，供后续的请求使用。配置 Random Variable 的步骤如下：

1.  在需要使用随机变量的 Sampler 或 Controller 上右键，选择添加 -> Config Element -> Random Variable。
    
2.  在 Random Variable 的属性窗口中，可以设置以下参数：
    

*   Variable Name：定义变量名，后续请求需要使用该变量名引用随机变量。比如，可以设置变量名为 randomNum。
*   Random Seed：指定随机数生成器的种子。默认情况下，种子使用当前时间戳。如果需要保证多次运行时生成的随机数相同，可以手动指定种子。
*   Minimum Value：设定随机数的最小值。如果需要生成字符串，则设定字符串的长度下限。
*   Maximum Value：设定随机数的最大值。如果需要生成字符串，则设定字符串的长度上限。
*   Format：指定随机数的格式，支持数字格式和字符串格式。比如，可以使用 #.## 表示生成两位小数的随机数，或者使用 AAA### 表示生成三个大写字母加三个数字的字符串。

3.  点击保存按钮，完成 Random Variable 的配置。

配置完成后，在后续的请求中可以使用 ${variableName} 的方式引用随机变量。比如，可以在 HTTP Request 中的 Path、Parameters、Body 等属性中使用 ${randomNum} 引用随机变量。在运行测试时，JMeter 会根据 Random Variable 的配置，生成指定范围内的随机数或字符串，并将其保存为变量。

---

Q: 如何通过随机变量的方式，让请求中的参数每次从ABCD中随机取一个

---

A: 可以通过在 JMeter 中添加 Random Variable 的方式，让请求中的参数每次从 ABCD 中随机取一个。具体步骤如下：

1.  在需要使用随机参数的 Sampler 或 Controller 上右键，选择添加 -> Config Element -> Random Variable。
    
2.  在 Random Variable 的属性窗口中，设置 Variable Name 为一个自定义的变量名，比如 letter。在 Minimum Value 和 Maximum Value 中，分别输入 1 和 4，表示从 1 到 4 中随机取一个数字。
    
3.  在需要使用随机参数的 Sampler 或 Controller 的请求参数中，使用 ${letter} 引用随机变量。
    
4.  运行测试，JMeter 会在每个线程中随机生成 1、2、3、4 中的一个数字，并将其作为 letter 变量的值。请求参数中使用 ${letter} 引用 letter 变量，从而实现每次请求时从 ABCD 中随机取一个参数的目的。
    

例如，如果需要发送一个 POST 请求，请求体为 letter=A、letter=B、letter=C、letter=D 中的一个，可以按照以下步骤配置：

1.  添加一个 HTTP Request。
    
2.  在 HTTP Request 中添加一个随机变量 Random Variable，设置 Variable Name 为 letter，Minimum Value 为 1，Maximum Value 为 4。
    
3.  在 HTTP Request 的 Body 中，使用 ${\_\_chooseRandom(A,B,C,D)} 引用随机参数。这里使用了 JMeter 内置函数 \_\_chooseRandom，它可以从多个参数中随机选择一个。注意，需要在函数中直接指定 ABCD 四个参数，而不是使用 ${letter} 引用 letter 变量。
    
4.  保存测试计划，运行测试即可。

---

