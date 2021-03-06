### 异步应用

### 异步到底是什么意思?

异步请求是指web服务器对请求作出响应时不要求你等待,这说明,你不会僵那里动弹不得,你可以继续做你想做的事情,并让服务器在处理完请求时通知你

### 你一直都在构建异步应用

实际网站的响应时间几乎总是比测试网站要慢,要明确应用的表现,唯一的办法就是在实际网站上测试你的应用

### 你能得出javascript需要向Mike的服务器发送什么?另外服务器端程序应当发回什么?

### 只需3个简单的步骤,实现(更多)异步性

1. 更新XHTML页面
   需要在增加两个口令域,一个用于输入口令,另一个用于检验该口令
2. 验证用户的口令
   接下来需要处理用户的口令,必须建立一个事件处理函数,它取一个口令作为参数,把口令发送给服务器,并建立一个回调来查看口令是否合法,然后类似用于户名域,可以使用同样的图标让用户知道他们的口令的合法
3. 提交表单
   最后,必须建立提交表单的代码,并在页面下方完成图像的动画,可以把这个代码关联到"Register"按钮的click事件,而不是通过一个正常的XHTML submit按钮来提交表单

### 为什么不使用addEventHander()来注册checkPassword()事件处理程序呢?
因为我们只向password2域指定一个事件处理程序,如果这个域 需要多个事件处理程序,那就该使用DOMLevel 2或者IE的attachEvent()了，如果是这样,你可能希望使用addEvent-Hander(),不过,由于这里事件只有一个事件处理程序,所以我们还是使用DOM level0

### 口令要作为Get请求的一部分发送吗?这样做安全?
对于现在来说,我们只强调异步的有关内容

### 利用一个请求对象,可以安全地发送和接收一个异步请求

使用了一个请求对象来建立两个异步请求,异步的含义是什么?异步是指两个请求不会等待浏览器或服务器的下一步动作,所以最后会用一个请求的数据覆盖另一个请求数据

但是,如果有两个异步请求怎么办?这两个请求不会相互等待,也不会让用户等待,每个请求对象都有自己的数据,而不是共享数据

### 这些与异步有什么关系?

如果炎症用户名的请求不是异步请求会怎么样?这样一来,在用户名请求完成之前就不可能发送口令请求,所以这个问题在同步坏境是不存在的

### 那么干脆让用户名请求作为一个同步请求不是更容易?

这样做确实会更容易,不过这样能得到最好的应用?如此一来,用户就必须等待用户名处理完,然后他们才能移到口令域，有时最简单的技术方案实际上是可用性最差的方案

### 为什么两个请求变量会共享同样的属性值?他们不是各自在不同的函数中声明为局部比变量

看起来是这样,但是实际上request最早是在createRequest()函数中定义的,不仅如此,request在createRequest()函数中定义时没有加var关键字,javascript中在函数内部声明的变量如果没有var关键字都会成为一个全局变量

### 那么为什么不直接在createRequest()中使用var关键字来修正这个问题?这样不就能使request成为局部变量了吗?

如果request是局部变量,那么回调函数如何访问请求对象？回调函数要求request是全局的,这样他们才能访问这个变量和他的属性值

### 那么请求赋值两个变量名有什么帮助?

在javascript中赋值采用复制方式处理,而不是按引用处理,所以将一个变量赋为另一个值时,新变量会得到所赋值变量的一个副本,javascript认为函数之外声明的所有变量以及声明时没有加var关键字的变量都是全局的,这些变量可以在任何地方由任何函数访问
在异步应用中,只检验用户输入的数据还不够,尽管会进行检验,你还必须对用户做出限制,如果未能通过检验,则不允许做只有通过检验后才能完成的动作

### 启用Rgister按钮怎么是限制的一般不分呢?这个不合逻辑
限制是指在检验完成之前不允许用户做某个动作的一个过程,所以启用一个按钮或激活一个表单是限制过程的一部分,实际上,每个限制过程的最后都是解除这个限制，异步意味着不能依赖于请求和响应的顺序,发送异步请求时,不能确定服务器会以什么样的顺序对这些请求作出响应,异步应用中绝对不要依赖于请求和响应的顺序或序列

### 可能需要采取行动时调用监视器函数
监视器函数通常用于根据多个变量更新应用或页面的某一部分,所以如果你认为可能需要更新一个页面时,比如说用户名或口令通过验证并返回时,就可以调用监视器函数

### 你能再解释一下监视器函数是什么?

当然可以,监视器函数就是一个监视应用的函数,所以,对于注册页面,监视器函数就要监视用户名和口令变量的状态,它会修改表单,从而与当前状态一致

### 我认为监视器函数通常会自动运行,比如说以一个固定的间隔运行

有时候确实如此,在更强调多线程功能的系统中,多线程功是指能够在后台运行的一个进程,通常会有一个监视器函数按一定的周期执行,这样一来就必像用户名和口令回调中那样显示的调用监视器函数,重构代码是抽取出代码中共同的本部分,并把这些部分放在一个易于维护的函数或方法中,重构可以使代码更易于更新和维护

### 为什么不在initPage()中声明usernameValid和passwordValid?

在所有函数之外声明的变量(有或者没有var)都是全局变量,在函数内部声明但是没有使用var关键字的变量也是全局的,在函数内部声明但是没有使用var关键字的变量也是全局的,在函数内部声明而且有var的变量则是全局变量,实际上,正是这个原因,我们将这两个变量放在所有函数之外的声明,这样可以更清楚的看出这两个变量是全局的,而不是任何特定函数内部的局部变量

### 那么为什么不同样在函数之外声明的usernameRequiest和passwordRequest?

这确实是一个很好的想法,而且你可能希望做此修改,在我们的代码中,这两个变量仍留在checkUsername()和checkPass-word()中,因为原来这些变量(原先名为request)就是在这些函数中创建的

### 难道不能在监视器函数中同时设置用户名和password1的状态？

当然可以,实际上,这也许是一个很好的想法,这说明代码中发生的css类修改会更少,大多数显示逻辑都由监视器函数处理

只要能够重构代码而不是导致太多不好的后果,那往往就是一个号的想法,更清晰的代码将易于修改和维护

### 同步请求会阻塞所有代码的工作

发送一个完整的表单进行处理时,通常希望这个请求是同步的,这是因为,你不希望用户在服务器正在处理数据时修改这些数据

### 要向服务器发送一个异步请求

最后,需要一个新的事件处理函数,这个函数需要得到一个新的请求对象,并把它发送到服务器,这应当是一个异步请求,从而当用户等待时可以完成动画滚动这些图像,你可以向客户建议候选方案,但是最终几乎总是要构建客户所要的应用,尽管你并不同意他们的决定

### 使用setInterval()让javascript运行你的进程,而不是由你自己的代码来运行

### 传入setInterval()的函数是一个回调函数?
没错,每次经过所设置的时间间隔后,就会由浏览器回调这里传入的函数

### 那么这个函数的编写与请求对象的回调函数一样?

这里不涉及请求对象,所以不需要检查任何readystate或status属性,另外这里没有要处理的服务器响应,所以只需一个每次调用时完成某个工作的javascript函数

### 这么说,在javascript中能做的事情在setInterval()回调函数中都可以做,对?

对于这个函数中能够什么没有任何限制

### 为什么指定函数时要使用括号?

因为不像原来指定事件处理程序那样,这里不是在设置一个属性,你要具体将代码传递给javascript解释器,解释器会在经过指定间隔后执行这些代码

### 这个回调会发生多少次？
在取消这个定时器之前会一直定期执行这个回调,可以利用clearInterval()取消定时器,可以向setInterval()传入任何javascript函数,以预定的时间间隔自动运行

### setInterval()实际上是javascript版本的多线程

有些编程语言,如c或者java,允许你指定在一个单独的线程中执行一个函数,如果计算机有多个cpu,那么两个不同的线程就可以同时执行,在大多数计算机上操作系统会在一段时间内执行一个线程,然后切换到另外一个线程,然后在回来执行前一个线程,这就像是开始时打手机,对我们来说,javascript解释器能够同时做两件事,一方面保证每隔几秒执行一次scrollImages(),另一方面处理我们的代码对我们的服务器做出异步请求


