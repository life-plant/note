#线程安全
当某个线程访问一种方法创建的数据时，该数据被锁定，不被其他数据访问改变时，则称为线程安全，否则为线程不安全；hashmap不是线程安全的，而ConcurrentHashMap是线程安全的