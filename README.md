sinaip
======
一个使用Sina的IP地址数据库

使用方法
------
数据已经全部用json格式化好了。
结构如下
class sinaip {
    long start_ip;
    long end_ip;
    long point;
    String country;
    String province;
    String city;
    String area;
    String ispType;
    String desc;
    String lat;
    String lnt;
}
其中 start_ip和end_ip都是以IP2Long形式展现，建议使用二分查找查找范围即可


Sample.java
------
    public static String searchIP(long ip) {
        int low = 0;
        int high = ip_db.size() - 1;
        while (low <= high) {
            int mid = (low + high) >>> 1;
            sinaip midIP = ip_db.get(mid);
            if (midIP.start_ip < ip && midIP.end_ip < ip) {
                low = mid + 1;
            } else if (midIP.start_ip > ip && midIP.end_ip > ip) {
                high = mid - 1;
            } else {
                return midIP.toString();
            }
        }
        return String.valueOf(-(low + 1));
    }
