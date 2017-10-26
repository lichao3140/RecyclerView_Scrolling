# RecyclerView常用封装、修复、嵌套滚动问题及优化
## RecyclerView 嵌套滑动问题
RecyclerView Big 嵌套RecyclerView Hor
最终是一个事件分发的问题。
### 问题一： 滑动没有根据斜率来计算
按键的分发，应该是分发给相对位移更大的RecyclerView。
但是，问题是，事件分发没有考虑到相对位移。
核心思想： 拦截onInterceptTouchEvent
### 问题二：当item 横线或者垂直滑动的时候，后面的事件没有被收到
## RecyclerView 优化
### 缓存机制
RecycledViewPool：一种用于多个RecyclerView之间共享View 的缓存。
应用场景：viewPager + adapter + tab 
private SparseArray<ArrayList<ViewHolder>> mScrap =
                new SparseArray<ArrayList<ViewHolder>>();
				
### RecyclerView 三级缓存：
#### 第一级缓存
##### a. mChangedScrap   RecyclerView中需要改变的Viewholder
##### b. mAttachedScrap  还没有和RecyclerView 分离的ViewHolder
##### c. mCachedViews    RecyclerView 的 ViewHolder 的缓存
#### 第二级
##### d. mViewCacheExtension   提供给开放者自己创建的缓存
#### 第三级
#####e. mRecyclerPool     缓存池
![](/screenshot/device-2017-10-26-210548.png)