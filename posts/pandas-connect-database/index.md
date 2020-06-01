# 使用 pandas 连接数据库


## 安装

```bash
pip install pandas
pip install sqlalchemy
pip install cx_oracle   # Oracle 引擎
pip install pymssql     # sql server 引擎
```

## 代码

```python
import pandas as pd
from sqlalchemy import create_engine


engine_name = "dialect+driver://user:password@host:port/dbname"
engine = create_engine(engine_name)
# 执行 SQL 语句
sql = "select * from table_name"
df = pd.read_sql_query(sql, engine)
# 将 DataFrame 数据上传数据库
pd.io.sql.to_sql(df, tb, con=engine, if_exists='append',
                         dtype=dtype, index=False)
```

