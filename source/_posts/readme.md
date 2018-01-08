## 为了增强程序的健壮性，管理运行时预见的错误-----异常
	1. 错误是程序不能执行 一般包括语法错误和逻辑错误
	2. 异常是程序出现了错误，而在正常控制流以外采取的措施
	- 异常处理的过程一般有两步，引发异常和处理异常
	- 处理异常 一般是直接pass或者执行一场之后的逻辑
## Python常见的异常
- NameError 当调用一个没有定义的变量时解释器出现的异常
	  >>> a
	  Traceback (most recent call last):
	  File "<stdin>", line 1, in <module>
	  NameError: name 'a' is not defined
- ZeroDivisionError 除数为0的error
- SyntaxError Python解释器语法错误
- indexError 序列的索引超标
- keyError 字典的键问题，字典中不存在键
- IOError 文件的异常，没有文件或者打开异常
- AttributeError 属性异常对象中没有属性

##异常的处理
1. try-except 如果try通过不执行except里面的逻辑
2. try-finally 不管try有没有通过都要执行finally里面的代码
3. try-except-finally
4. try-except-else-finally

## 例子 返回浮点型
 
    def safe_float(obj):
      try:
         return float(obj)
      except ValueError, e:
         return 'ValueError', e
      except TypeError, e:
         return 'TypeError', e

     F:\Python2\python.exe F:/pycode/Error/handle_error.py
	('TypeError', TypeError('float() argument must be a string or a number',))
	('ValueError', ValueError('could not convert string to float: xxxx',))

## 捕获多处异常和异常参数
	   def safe_float1(obj):
	    try:
	        return float(obj)
	    except (TypeError, ValueError), dig:
	        print type(dig)
	        print dig
	        return str(dig)

       <type 'exceptions.TypeError'>
		float() argument must be a string or a number
		float() argument must be a string or a number




