# Core Java Learning Notes

## Chapter 4

### 4.4 静态域与静态方法

#### 20180619

1. 静态方法可直接通过类名调用。静态方法没有this隐式参数。
2. 需要使用静态方法的2种情况：
    - 一个方法不需要访问对象状态，其所需参数都是通过显式参数提供（例如： Math.pow)。
    - 一个方法只需要访问类的静态域（例如：Employee.getNextldh