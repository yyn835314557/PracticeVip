#Essay
***
- hasOwnProperty: 该方法属于 object 对象，所有对象都 "继承" object对象实例
    - 判断该对象是否有你给出的属性或对象(true,false)
    - 此方法无法检查该对象的原型链中是否具有该属性，该属性必须是对象本身的一个成员。
    - object.hasOwnProperty(propertyName)
- isPrototypeOf:
    - 判断要检查其原型链的对象是否存在于指定的对象实例中(true ,false)    