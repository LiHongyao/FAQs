### 001：简述什么事BFC？

1. 基本概念：**B**lock **F**ormatting **C**ontext，块级格式化上下文

   它是一个独立的布局环境，其中的元素布局不会影响到外界元素； 

2. 解决什么问题？

   - 外边距重叠问题；（例如给一个元素添加 overflow:hidden) 
   - 浮动元素引起的父元素高度塌陷问题（也就是清除浮动）
   - 两栏自适应布局

3. 满足以下条件，就可以创建BFC

   - 浮动元素：float 值 不为 none；
   - 定位元素：position 为 absolute 或 fixed；
   - 内联块：display 为 inlin-block/table-cell/flex/grid；
   - overflow：值不为 visible；

