# php-Keyword

php常用关键字-常用魔术方法

  
  PHP中常用的关键字
  	
  	final
  		  1. final不成修饰成员属性（类中常不是用这个关键字）
  		  2. final只能修饰类和方法
 
  		作用：
  			使用final修饰的类 不 能被子类继承
  			使用final修饰的方法不能被子类去覆盖
 
  			用来限制类不被继承，方法不被覆盖就使用fianl
 
  	static
  		    1. 使用static可以修饰成员属性和成员方法，不能修饰类
 
  		    2. 用static修饰的成员属性，可以被同一个类的所有对象共享
 		
 		      3. 静态的数据是存在 内存中的 数据段中（初使化静态段）
 
 		      4. 静态的数据是在类第一次加载时 分配到内存中的， 以后再用到类时就直接从数据段中获取
 
 		      5. 什么是类被加载？ 只要在程序中使用到这个类（有这个类名出现）
 
	注意： 静态的成员都要使用类名去访问，不用创建对象, 不用对象去访问
 			
          类名::静态成员

          如果在类中使用静态成员， 可以使用 self代表本类（$this是代表本对象）

  		
 
 
 		6. 静态方法（static修饰的方法）， 不能访问非静态的成员（在非静态的方法中，可以访问静态成员）

          因为非静态的成员， 就必须用对象来访问，访问内部的成员使用的就是$this

          静态方法 不用使用对象来调用， 也就没有对象， $this也就不能代表什么对象， 非静态的成员还必须使用对象

          如果你确定一个方法不使用非静态的成员， 则可以将这个方法声明为 静态方法（不能创建对象，直接使用类名就可以访问）		


    			静态成员： 类名::成员 ， 在类内部访问其它成员 self::成员
 
 
 			
 
        const
            1. 他只能修饰成员属性

          define('HOST', 'www.xsphp.com');

          2. 类中声明常量属性使用const

          3. 命名的方式和我们以前学习 define是一样的效果

          4. 访问方式和static静态成员属性是一样（在类外部使用  类名::常量， 在类内部使用  self::常量）

          5. 常量一定要在声明时就给初值
 
 
 
  PHP中常用的魔术方法

          __call() 

            作用: 在调用对象中不存在的方法时就会出现系统报错，然后程序退出。

            什么时候自动调用: 就会在调用一个对象中不存的的方法时自动调用

            处理一些不存在方法的错误调用

            这个方法需要两个参数  第一个参是代表函数名字，第二个参数代表函数形参

            __toString()
              直接输出对象引用时自动调用， 用来快速获取对象的字符串表示的最便捷的方式


            __clone()
              克隆对象使用clone去处理

              原本 （原来的对象）

              复本 （复制出来的对象）

 
            __clone()就是在克隆对象时自动调用的方法


            只要一个对象一诞生，就要有初使化的动作， 和构造方法__construct作用相似

            在__clone()方法中的 $this关键字，代表的是复本, $that代表原本对象


          __autoload()
            注意： 其它的魔术方法都是在类中添加起作用， 这是一个唯一一个不在类中添加的方法

            只要在页面中使用到一个类，只要用到类名就会自动将类名传给这个参数


              对象串行化（序列化）： 将一个对象转为二进制串 （对象是存储在内存）

                     1. 将对象长时间存储在数据库或文件中时
                     2. 将对象在多个PHP文件中传输时

            serialize() : 参数是一个对象， 返回来的就是串行化后的二进制串	
            unserialize() : 参数就是对象的二进制串， 返回来的就是新生成的对象

            __sleep()

              是在序列化时自动调用的方法

            作用：就是可以将一个对象部分串行化

              只要这个方法中返回一个数组，数组中有几个成员属性就序列化几个成员属性，如果不加这个方法，则所有成员都被序列化
              
            __wakeup()

              是在反序列化时自动调用的方法

              也是对象重新诞生的一个过程(__construct(), __clone(),__wakeup())






          __call() 

		    作用: 在调用对象中不存在的方法时就会出现系统报错，然后程序退出。

		    什么时候自动调用: 就会在调用一个对象中不存的的方法时自动调用

		    处理一些不存在方法的错误调用

		      这个方法需要两个参数：  第一参数是：函数名      第二个参数是：函数参数



			   class Pres{
					private  $name;
					private	  $age;
					private   $sex;
					const HOST="localhost";
				function __construct($name,$age,$sex){
					$this->name=$name;
					$this->age=$age;
					$this->sex=$sex;
				}

				function text(){
					echo "我的名字：{$this->name},我的年龄：{$this->age},我的性别：{$this->sex}";
				}
				function text2(){
					echo'0000000000000000000<br>';
				}

				function __call($methodName, $args){
					echo"没有这个方法 {$methodName},<br> 参数 ";
				    print_r($args);
				     echo "不存在 <br>";
				  }
			    }

				$p=new Pres('张三',90,'nan');
				$p->text1();
				$p->text33("ppp");
				$p->text55();
				
				
				  输出     
						没有这个方法 text1,
						参数 Array ( ) 不存在 
						没有这个方法 text33,
						参数 Array ( [0] => ppp ) 不存在 
						没有这个方法 text55,
						参数 Array ( ) 不存在 




    __clone()就是在克隆对象时自动调用的方法
    

					   class Pres{
							public  $name;
							public	  $age;
							public   $sex;
							const HOST="localhost";
						function __construct($name,$age,$sex){
							$this->name=$name;
							$this->age=$age;
							$this->sex=$sex;
						}

						function text(){
							echo "我的名字：{$this->name},我的年龄：{$this->age},我的性别：{$this->sex}<br>";
						}
						//给克隆对象重新初始化
						function __clone(){
							$this->name='李四';
							$this->age=100;
							$this->sex='男';
						}
					    }

						$p=new Pres('张三',90,'女');

						克隆$p;
						$p1= clone $p;

						输出原来的对象的值
						$p->text();          //我的名字：张三,我的年龄：90,我的性别：女

						输出克隆后的值
						$p1->text();       //我的名字：李四,我的年龄：100,我的性别：男




 __autoload()
 
 
 
			    注意： 其它的魔术方法都是在类中添加起作用， 这是一个唯一一个不在类中添加的方法

			    只要在页面中使用到一个类，只要用到类名就会自动将类名传给这个参数



                             one.class.php  文件


				<?php
				  class One{
					function fun1(){
					echo "我是one 11111111111111111<br>";
				 }
			       }

			     ?>
				

				two.class.php   文件
				
				
				    <?php
					class Two{
					static	function fun2(){
							echo "我是two 22222222<br>";
						}
					}	
				   ?>	
				
				
				three.class.php
				
				<?php
				     class Three{
					function fun3(){
						echo "我是three 33333333 <br>";
					}
				 }
				?>
				
		           texts.php  文件  输出页面
			    
			         <?php
					@header("content-Type: text/html; charset=utf-8");
					function  __autoload($url){
						include "./".$url.".class.php";
					}

						 $p1=new One;
						 $p1->fun1();   //输出        我是one 11111111111111111

						Two::fun2();    //输出      我是two 22222222

						$p2=new Three;
						$p2->fun3();   // 输出      我是three 33333333

				 ?>
	
	
	
	
				
 对象串行化（序列化）： 将一个对象转为二进制串 （对象是存储在内存）
 
 
      		   1. 将对象长时间存储在数据库或文件中时
      		   2. 将对象在多个PHP文件中传输时
 
 		serialize() : 参数是一个对象， 返回来的就是串行化后的二进制串	
 		unserialize() : 参数就是对象的二进制串， 返回来的就是新生成的对象
 
 	__sleep()
 
  		是在序列化时自动调用的方法

		作用：就是可以将一个对象部分串行化

		     只要这个方法中返回一个数组，数组中有几个成员属性就序列化几个成员属性，如果不加这个方法，则所有成员都被序列化
 	__wakeup()
 	
 		是在反序列化时自动调用的方法
      
 		也是对象重新诞生的一个过程(__construct(), __clone(),__wakeup())				
				
				
				
		   dome 文件		
				
		         <?php

			   class Pres{
					public  $name;
					public	  $age;
					public   $sex;
					const HOST="localhost";
				function __construct($name,$age,$sex){
					$this->name=$name;
					$this->age=$age;
					$this->sex=$sex;
				}

				function text(){
				   echo "我的名字：{$this->name},我的年龄：{$this->age},我的性别：{$this->sex}<br>";
				}
				

		    __sleep		
			作用：就是可以将一个对象部分串行化
		           只要这个方法中返回一个数组，数组中有几个成员属性就序列化几个成员属性，
                           如果不加这个方法，则所有成员都被序列化
		
				function __sleep(){
				return array("name", "age");   // 我的名字：张三,我的年龄：10,我的性别：     这里sex就是忽略了

				}	
					
			       在反序列化时自动调用的方法 , 在反序列化 重新初始化   
			      function __wakeup(){
				$this->name="三张";
				$this->age=$this->age-1;         //我的名字：三张,我的年龄：9,我的性别：
			      }
			 }

		  ?>

	
	

			write.php 文件    写的文件

			<?php

			require "dome.php";

			$p=new Pres('张三', 10, '男');

			// serialize 转成二进制的串 (序列化)
			 $str=serialize($p);

		      // file_put_contents :写      把$str里面的数据写到mess.txt文件里面
			 file_put_contents("mess.txt", $str);

			?>  
	  
	               read.php   读的文件
	  
			  <?php
				require "dome.php"; // Person Class
				//file_get_contents   读
				$str=file_get_contents("mess.txt");

				//unserialize反序列化 字符串
				$pp=unserialize($str);
				$pp->text();
				
				 输出    我的名字：三张,我的年龄：9,我的性别：

			 ?>
	  
	  
	  
	  
	  
	  
	  
	  
	  
		


