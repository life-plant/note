#StringBuffer原生类
    StringBuffer strbuf = new StringBuffer("str1");
    开拓一个新的缓存区域，创建可变字符
    strbuf.append("str2") ===>"str1str2"
    strbuf.insert(offset=4,"str3"); ===> "str1str3str2"
    strbuf.toString(); 创建真正的字符串，不可变了；