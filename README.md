# springbean-InitializingBean-order

一、Spring装配Bean的过程   
  1. 实例化;  
  2. 设置属性值;  
  3. 如果实现了BeanNameAware接口,调用setBeanName设置Bean的ID或者Name;  
  4. 如果实现BeanFactoryAware接口,调用setBeanFactory 设置BeanFactory;  
  5. 如果实现ApplicationContextAware,调用setApplicationContext设置ApplicationContext  
  6. 调用BeanPostProcessor的预先初始化方法;  
  7. 调用InitializingBean的afterPropertiesSet()方法;  
  8. 调用定制init-method方法；  
  9. 调用BeanPostProcessor的后初始化方法;  

Spring容器关闭过程   
  1. 调用DisposableBean的destroy();  
  2. 调用定制的destroy-method方法;


一，单一Bean
  装载
  1. 实例化;  
  2. 设置属性值;  
  3. 如果实现了BeanNameAware接口,调用setBeanName设置Bean的ID或者Name;  
  4. 如果实现BeanFactoryAware接口,调用setBeanFactory 设置BeanFactory;  
  5. 如果实现ApplicationContextAware,调用setApplicationContext设置ApplicationContext  
  6. 调用BeanPostProcessor的预先初始化方法;  
  7. 调用InitializingBean的afterPropertiesSet()方法;  
  8. 调用定制init-method方法；  
  9. 调用BeanPostProcessor的后初始化方法; 

spring容器关闭
  1. 调用DisposableBean的destroy();  
  2. 调用定制的destroy-method方法;
 
二，多个Bean的先后顺序
  1. 优先加载BeanPostProcessor的实现Bean;
  2. 按Bean文件和Bean的定义顺序按bean的装载顺序（即使加载多个spring文件时存在id覆盖）;
  3. “设置属性值”（第2步）时，遇到ref，则在“实例化”（第1步）之后先加载ref的id对应的bean;
  4. AbstractFactoryBean的子类，在第6步之后,会调用createInstance方法，之后会调用getObjectType方法;
  5. BeanFactoryUtils类也会改变Bean的加载顺序;
