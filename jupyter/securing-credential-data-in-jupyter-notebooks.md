# Securing Credential Data in Jupyter Notebooks

Jupyter is pretty amazing for collecting and analyzing data.  If you’re going to be hooking up to a database for raw data, and who wouldn’t, credentials suddenly become real.  

If you want to push the results out to the big wide world web filled with bad actors, then it’s a super good time to research credential management.  

A very thorough article on Medium was written by Heang Yuthakarn Arngmaneekul - see [post](https://medium.com/@yuthakarn/how-to-not-show-credential-in-jupyter-notebook-c349f9278466).

In short, the hot secrets are kept in a .env file which contains the super secret jewels of the universe.  This file is stored in the Jupyter lab directory and isn’t readily visible.  Best of all, it won’t be included with when working with Jupyter on Github. 

His example is a great template:

```python
from dotenv import load_dotenv
import os
import sqlalchemy as db
load_dotenv()
user = os.getenv('MYSQL_USER')
password = os.getenv('MYSQL_PASSWORD')
host = os.getenv('MYSQL_HOST')
db = os.getenv('MYSQL_DB')
conn_text = 'mysql://{}:{}@{}/{}'.format(user,password,host,db)'
engine = db.create_engine(conn_text)
```
