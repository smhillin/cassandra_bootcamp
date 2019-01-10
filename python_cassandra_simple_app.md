



## create a file python_cass_lab.py with the following code

  import logging
  from cassandra import ConsistencyLevel
  from cassandra.cluster import Cluster, BatchStatement
  from cassandra.query import SimpleStatement


  class PythonCassandraExample:

      def __init__(self):
          self.cluster = None
          self.session = None
          self.keyspace = None
          self.log = None

      def __del__(self):
          self.cluster.shutdown()

      #connect to cluster
      def createsession(self):
          self.cluster = Cluster(['localhost'])
          self.session = self.cluster.connect(self.keyspace)

      def getsession(self):
          return self.session

      # Add some log info
      def setlogger(self):
          log = logging.getLogger()
          log.setLevel('INFO')
          handler = logging.StreamHandler()
          handler.setFormatter(logging.Formatter("%(asctime)s [%(levelname)s] %(name)s: %(message)s"))
          log.addHandler(handler)
          self.log = log

      # Create Keyspace based on Given Name
      def createkeyspace(self, keyspace):

          # Create new keyspace
          rows = self.session.execute("SELECT keyspace_name FROM system_schema.keyspaces")
          if keyspace in [row[0] for row in rows]:
              self.log.info("dropping existing keyspace...")
              self.session.execute("DROP KEYSPACE " + keyspace)

          self.log.info("creating keyspace...")
          self.session.execute("""
                  CREATE KEYSPACE %s
                  WITH replication = { 'class': 'SimpleStrategy', 'replication_factor': '2' }
                  """ % keyspace)

          self.log.info("setting keyspace...")
          self.session.set_keyspace(keyspace)

      def create_table(self):
          c_sql = """
                  CREATE TABLE IF NOT EXISTS students (st_id int PRIMARY KEY,
                                                name varchar,
                                                age int ,
                                                city varchar);
                   """
          self.session.execute(c_sql)
          self.log.info("Students Table Created !!!")

      # lets do some batch insert
      def insert_data(self):
          insert_sql = self.session.prepare("INSERT INTO  students (st_id, name , age,city) VALUES (?,?,?,?)")
          batch = BatchStatement()
          batch.add(insert_sql, (1, 'Shaun', 38, 'Austin'))
          batch.add(insert_sql, (2, 'Meghan', 34, 'Toronto'))
          batch.add(insert_sql, (3, 'Jamal', 24, 'Chicago'))
          batch.add(insert_sql, (4, 'Mohamed', 32, 'San Francisco'))
          self.session.execute(batch)
          self.log.info('Batch Insert Completed')

      def select_data(self):
          rows = self.session.execute('select * from students limit 4;')
          for row in rows:
              print(row.name, row.city)

      def update_data(self):
          pass

      def delete_data(self):
          pass


  if __name__ == '__main__':
      example1 = PythonCassandraExample()
      example1.createsession()
      example1.setlogger()
      example1.createkeyspace('cass_py_lab')
      example1.create_table()
      example1.insert_data()
      example1.select_data()
      
## Run the python file in your terminal

  python python_cass_lab.py

## You should see something like this result

  2019-01-10 17:28:49,778 [INFO] root: dropping existing keyspace...
  2019-01-10 17:28:51,195 [INFO] root: creating keyspace...
  2019-01-10 17:28:51,875 [INFO] root: setting keyspace...
  2019-01-10 17:28:52,510 [INFO] root: Students Table Created !!!
  2019-01-10 17:28:52,540 [INFO] root: Batch Insert Completed
  (u'Shaun', u'Austin')
  (u'Meghan', u'Toronto')
  (u'Mohamed', u'San Francisco')
  (u'Jamal', u'Chicago')
  
## Try to edit the code for the below scenario

1.  Create a new table called "classes" and 
2.  Create columns that represent the class name, max enrollment, campus, teacher, course number
3.  Choose a Primary Key
4.  Add 5 entrys to those tables.  Assume there are two compuses North and South.
5.  Query the table and return classes on South campus.
6.  Print class and teacher to screen.

## Run your Python Program and View Your Results
