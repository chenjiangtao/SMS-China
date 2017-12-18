SMS-China
=========

~~中国移动CMPP、联通SGIP、电信SMGP三网合一企业短信网关~~
# 中国移动CMPP、电信SMGP两个模块

文档下载 http://222.66.24.235:8080/ctmp/file/api.zip

java sample code:

    public class SMGPTester {
        private static Logger log = LogManager.getLogger(SMGPTester.class);
        private static final SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss:SSS");
    
        public static void main(String[] args) {
            SMGPConnection conn = new SMGPConnection();
            conn.setClientId("aaa021");
            conn.setPassword("aaa123");
            conn.setVersion((byte) 0);
            conn.setAutoReconnect(true);
            conn.setSendInterval(200);
    
            conn.connect("222.66.24.235", 8900);
            //conn.connect("127.0.0.1", 8900);
    
            if(conn.isConnected()){
    
                Session session = conn.getSession();
    
                String[] phones = new String[] { "1316264XXXX" };
    
                long startTime = System.currentTimeMillis();
                try {
                    for(int i = 0; i < 1; i++) {
                        String content = String.format("第%d条:电信smgp测试Z(%s)", i+1, format.format(new Date()));
                        session.submit(content, "1065902100612", phones[i/10]);
                    }
                }
                finally {
                    log.info(String.format("total:%d",System.currentTimeMillis()-startTime));
                    /*
                    try {
                        Thread.sleep(10000L);
                    }
                    catch (InterruptedException ex) {}
                    try {
                        session.close();
                    }
                    catch (IOException ex){
                    }
                    */
                }
            }
        }
    }
    

    
