1. http://blog.csdn.net/v_july_v/article/details/11288807
2. http://www.cnblogs.com/step1/archive/2009/04/22/1441689.html
3. https://charlee.li/geohash-intro.html

### geohash的应用：附近地址搜索

geohash的最大用途就是附近地址搜索了。不过，从geohash的编码算法中可以看出它的一个缺点：位于格子边界两侧的两点， 虽然十分接近，但编码会完全不同。
实际应用中，可以同时搜索当前格子周围的8个格子，即可解决这个问题。
