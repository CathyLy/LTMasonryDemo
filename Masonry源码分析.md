### Masonry源码分析
    Masonry是对NSLayoutContraint的封装
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/Masonry.png)

类目:

    View+MASAdditions
    MASViewAttribute
    MASViewConstraint
    MASConstraintMaker

 
#### 一.View+MASAdditions
    mas_makeConstraints:创建安装约束,返回值是一个数组存储的是MASViewConstraint对象
    mas_updateConstraints:更新已经存在的约束（若约束不存在就Install)
    mas_remakeConstraints:移除原来已经创建的约束并添加上新的约束
    mas_closestCommonSuperview:寻找两个视图的最近的公共父视图
    
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/View%2BMASAdditions.png)

#### 二.MASViewAttribute 
    这个类是对UIView和NSLayoutAttribute的封装,是view和NSLayoutAttribute的合体
    @property view 表示所约束的对象
    @property item  该view对象上可以被约束的部分,在NSLayoutConstriant构造器中作为constraintWithItem与toItem的参数,
    
    @property layoutAttribute
    initWithView:layoutAttribute:  
    initWithView:item:(id)item layoutAttribute:
    isSizeAttribute:用来判断MASViewAttribute类中的layoutAttribute属性是否是NSLayoutAttributeWidth或者NSLayoutAttributeHeight,
                    如果是,则约束添加到当前View上
    
#### 三.MASViewConstraint
    MASViewConstraint是对NSLayoutConstraint类的进一步封装,核心的事件就是初始化NSLayoutConstraint对象,并将该对象添加到相应的视图上
    NSLayoutConstriant初始化需要NSLayoutAttribute和所约束的View,所以NSLayoutConstriant类依赖于MASViewAttribute

#### 四.MASConstraintMaker
    负责创建MASConstraint类,并调用MASConstraint对象的install方法来将相应的约束安装到想要的视图上
    View+MASAdditions中就是调用MASConstraintMaker中的一些方法
    每个MASConstraint类型的属性都对应一个getter方法,getter方法会调用addConstraintWithLayoutAttribute
    
    - (MASConstraint *)baseline {
    return [self addConstraintWithLayoutAttribute:NSLayoutAttributeBaseline];
    }
    
    
如下是MASConstraintMaker工厂方法解析:
![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/MASConstraintMaker.png)

工厂类中的install方法:

![image](https://raw.githubusercontent.com/CathyLy/imageForSource/master/MASConstraintMaker_install.png)
    
    

