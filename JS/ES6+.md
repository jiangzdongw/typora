1. ES新提案：可选链(?.)和双问号(??)

   ES新提案：可选链(?.)和双问号(??) - K先生的文章 - 知乎 https://zhuanlan.zhihu.com/p/113123170

2. JS 常用继承方法。

   原型链继承+构造函数实现类的继承。https://www.cnblogs.com/qing-5/p/11365614.html

   **一、原型链实现继承**

    **原型链实现继承的思想**：利用原型让一个引用类型继承另一个引用类型的属性和方法。

    **原型链的基本概念**： 当一个原型对象等于另一个类型的实例，此时的原型对象将包含一个指向另一个指向另一个原型的指针。同时，另一个原型中也包含着一个指向另一个构造函数的指针。如果另一个原型是另一个类型的实例，此时实例和原型就构成了原型链

   

   ```javascript
   function SuperType(){
         this.property=true;
   }
   SuperType.prototype.getSuperValue=function(){
         return this.property;
   }
   function SubType(){
         this.subproperty=false;
   }
   //通过创建SuperType的实例继承了SuperType
   SubType.prototype=new SuperType();
   
   SubType.prototype.getSubValue=function(){
         return this.subproperty;
   }
   var instance=new SubType();
   alert(instance.getSuperValue());  //true                                      
   ```

   

   **对于代码的解释：**

   首先定义了两个类型SuperType和SubType。此时SubType通过创建SuperType的实例（**new** **SuperType()**），并将该实例（**new** **SuperType()**）赋给了SubType的原型SubType.prototype的方式  继承了 SuperType。

   此时存在于SuperType中实例中的所有属性和方法，也存在于SubType.prototype中。此时，实例、原型和构造函数之间的关系如下图所示。

    SubType的实例**instance**指向SubType的原型SubType.prototype，SubType.prototype又指向SuperType的原型。

   **注意**：getSuperValue()方法仍然还在SuperType.prototype中，但property则位于SubType.prototype中。这是因为property是一个实例属性，而getSuperValue()则是一个原型方法。

   ![img](https://img2018.cnblogs.com/blog/1179017/201908/1179017-20190816201427785-2058373653.png)

   **原型链存在的问题：**

    1）包含引用类型值的原型属性会被所有实例共享，这会导致对一个实例的修改会影响另一个实例。在通过原型来实现继承时，原型实际上会变成另一个类型的实例。原先的实例属性就变成了现在的原型属性

   （2）在创建子类型的实例时，不能向超类型的构造函数中传递参数

   **二、借用构造函数\**实现继承\****

   **借用构造函数**的**基本思想**，即在子类型构造函数的内部调用超类型构造函数。函数只不过是在特定环境中执行代码的对象，因此通过使用apply()和call()方法可以在新创建的对象上执行构造函数。

   ```javascript
   function SuperType(){
         this.colors=["red", "blue", "green"];
   }
   function SubType(){
         //继承SuperType
         SuperType.call(this);
   }
   var instance1=new SubType();
   instance1.colors.push("black");
   alert(instance1.colors);  //red,bllue,green,black
   
   var instance2=new SubType();
   alert(instance2.colors);  //red,blue,green
   ```

   **代码的解释：**

   ```
    SuperType.call(this);“借调”了超类型的构造函数。通过使用call()方法（或者apply()方法），在新创建的SubType实例的环境下调用了SuperType构造函数。这样一来就会在新的SubType对象上执行SuperType()函数中定义的所有对象初始化代码。结果，SubType的每个实例都会有自己的colors属性副本
   ```

   **借用构造函数的优势：**可以在子类型构造函数中向超类型构造函数传递参数

   ```javascript
   function SuperType(name){
         this.name=name;
   }
   function SubType(){
         //继承了SuperType,同时还传递了参数
         SuperType.call(this,"mary");//this（SubType的实例）调用SuperType构造函数
         //实例属性
         this.age=22;
   }
   var instance=new SubType();
   alert(instance.name);  //mary
   alert(instance.age);  //29
   ```

   **借用构造函数的问题：**

   1）无法避免构造函数模式存在的问题，方法都在构造函数中定义，因此无法复用函数。

   2）在超类型的原型中定义的方法，对子类型而言是不可见的。因此这种技术很少单独使用。

   **三、组合继承**

   **组合继承：**指的是将原型链和借用构造函数的技术组合到一起。思路是使用原型链实现对原型方法的继承，而通过借用构造函数来实现对实例属性的继承。这样，既通过在原型上定义方法实现了函数的复用，又能够保证每个实例都有它自己的属性。

   ```javascript
   
   
   instance1.colors.push("black");
   alert(instance1.colors);   //red,blue,green,black
   instance1.sayName();  //mary
   instance1.sayAge();  //22
   
   var instance2=new SubType("greg", 25);
   alert(instance2.colors);   //red,blue,green
   instance2.sayName();  //greg
   instance2.sayAge();  //25
   ```

   **代码解释：**

    SuperType构造函数定义了两个属性：name和colors。SuperType的原型定义了一个方法sayName（）。

    SubType构造函数在调用SuperType构造函数时传入了name参数。并定义了自己的属性age。

   ```
   然后，将SuperType实例赋值给SubType的原型，然后又在新原型上定义了sayAge方法。
   此时可以让两个不同的SubType实例分别拥有自己的属性，又可以使用相同的方法
   组合继承的优势：
   避免了原型链和借用构造函数的缺点，融合了他们的优点，是JavaScript中最常用的继承模式。instanceof和isprototypeOf()也能够用于识别基于组合继承创建的对象
   ```

    