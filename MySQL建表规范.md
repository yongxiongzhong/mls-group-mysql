##表定义规范
###命名
1. 库名、表名、字段名使用小写字母，“_”分割。
2. 库名、表名、字段名不超过 12 个字符。
3. 库名、表名、字段名见名知意,尽量使用名词儿不是动词。
4. 不能使用数据库保留字,比如：key，desc，delete，order
5. 按时间分表。按年分表，table_name_YY、按月分表table_name_YYMM、按日分表table_name_YYMMDD(例：table_name_2016、 table_name_201601、 table_name_20160101)
6. 普通分表表名称原则同上，散表以下划线+数字结尾，例如：table_0,table_1.......table_99

###存储引擎
1. 默认选择innoDB
2. 如果选择其他引擎的需求、找DBA审核

###字符集
表字符集选择 UTF8

##表设计规范
###共同规范
1. 字段定义为NOT NULL、因为NULL在MySQL中得特殊处理、很难优化
2. 将大字段拆分值其他表中
3. 不在数据库中使用字段存储图片、媒体、文件等、只存储路径

###数值类型规范
1. 使用 UNSIGNED 存储非负数值、存储范围可以提升一倍
2. 整型定义中不添加长度,比如使用 INT,而不是 INT(4)。INT(SIZE)中的SIZE是指显示宽度，不影响存储范围
3. 小的整型定义、比如状态类、统一使用TINYINT表示，不建议使用ENUM、SET 类型
4. 使用 INT UNSIGNED 存储 IP。IP转数字函数inet_aton()、数字转IP函数inet_ntoa()
5. 存储精确浮点数必须使用 DECIMAL 替代 FLOAT 和 DOUBLE
6. FLOAT/DOUBLE/DECIMAL(Length, Decimals)。Length表示总长度、Decimals表示精度(小数点后Decimals位)

###字符串类型规范
1. VARCHAR(N)中的N表示字符数(不是字节数、比如VARCHAR(N)能存储N个汉字)、满足需求的情况下N越小越好、最大长度65535个字节
2. 对于定长的字符类型、比如密码MD5值等、建议用char类型。效率可以得到提升
3. 引用场景下当列的最大长度比平均长度大很多，并且列很少更新的时候用vachar、效率可以得到提升

###时间类型规范
1. 存储年份使用YEAR类型
2. 存储日期使用DATE类型
3. 存储时间使用DATETIME类型


##【FAQ】

