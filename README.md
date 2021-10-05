# Apache-Flume-Installation-Twitter-Data-Streaming-on-Hadoop
YÊU CẦU: ĐÃ CÀI ĐẶT SẴN: HADOOP, JDK(Oracle JDK), OpenSSH

1. Extract Flume và đưa vào thư mục home

2. Thiết lập đường dẫnfile “.bashrc”
export FLUME_HOME=/home/<use_name>/apache-flume-1.9.0-bin
export PATH=$PATH:$FLUME_HOME/bin

	=> Cập nhật lại file “.bashrc”

3. Tạo file twitter.conf trong thư mục /apache-flume-1.9.0-bin/conf:
Tiến hành Config file:

# Name the components on this agent
TwitterAgent.sources = Twitter
TwitterAgent.channels = MemChannel
TwitterAgent.sinks = HDFS

# Source
TwitterAgent.sources.Twitter.type= org.apache.flume.source.twitter.TwitterSource
TwitterAgent.sources.Twitter.channels = MemChannel
TwitterAgent.sources.Twitter.consumerKey = <consumerKey>
TwitterAgent.sources.Twitter.consumerSecret = <consumerSecret>
TwitterAgent.sources.Twitter.accessToken  = <accessToken >
TwitterAgent.sources.Twitter.accessTokenSecret= <accessTokenSecret> 
TwitterAgent.sources.Twitter.keywords = hadoop, big data, analytics, bigdata, mapreduce
# Sink
TwitterAgent.sinks.HDFS.channel = MemChannel
TwitterAgent.sinks.HDFS.type = hdfs
TwitterAgent.sinks.HDFS.hdfs.path= hdfs://localhost:9000/user/<user-name>/ <đường dẫn đến thư mục hdfs>
TwitterAgent.sinks.HDFS.hdfs.fileType = DataStream
TwitterAgent.sinks.HDFS.hdfs.writeFormat = Text
TwitterAgent.sinks.HDFS.hdfs.batchSize = 1000
TwitterAgent.sinks.HDFS.hdfs.rollSize = 0
TwitterAgent.sinks.HDFS.hdfs.rollCount = 10000

# Channel
TwitterAgent.channels.MemChannel.type = memory
TwitterAgent.channels.MemChannel.capacity = 10000
TwitterAgent.channels.MemChannel.transactionCapacity = 10000

Với Keys and tokens trên tài khoản Twitter Applications.
    hdfs.path đường dẫn đến thư mục HDFS lưu trữ bạn lưu dữ liệu.

4. Khởi động NameNode và DataNode, ResourceManager và NodeManager
   Run Flume:
flume-ng agent -n TwitterAgent -c conf -f apache-flume-1.9.0-bin/conf/twitter.conf -property flume.root.logger=DEBUG,console
CRTL+C để dừng Kiểm tra kết quả

5. KẾT THÚC.
   
