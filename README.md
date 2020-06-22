Create test data

%python
####FUNCTIONS
import pandas as pd
from faker import Factory
import pandas as pd
import random

from faker import Faker
fake = Faker()

###VARIABLE DEFINITIONS
c_current_cdemo_sk = ["c1", "c2", "c3", "c4", "c5"]
c_current_hdemo_sk = ["h1", "h2", "h3", "h4", "h5"]
salutations = ["Mr.", "Mrs.", "Ms", "Dr", "Prof", "None"]
print("c_customer_id : ", fake.uuid4())
print("c_customer_sk : ", fake.sha256())
print("c_current_cdemo_sk : ", fake.words(1, c_current_cdemo_sk, True))
print("c_current_hdemo_sk : ", fake.words(1, c_current_hdemo_sk, True))
print("c_current_addr_sk : ", fake.address())
print("c_first_shipto_date_sk", fake.date())
print("c_first_sales_date_sk", fake.date())
print("c_salutation : ", fake.words(1, salutations, True)[0])
print("c_first_name : ", fake.first_name())
print("c_last_name : ", fake.last_name())
print("c_preferred_cust_flag : ", fake.words(1, ["Y", "N"], True)[0])
print("c_birth_year : ", fake.year())
print("c_birth_country : ", fake.words(1, ["AB", "BC", "CD"], True)[0])
print("c_email_address : ", fake.email())
print("c_last_review_date : ", fake.date())


df1 = pd.DataFrame(columns=("c_customer_id", "c_customer_sk", "c_current_cdemo_sk", "c_current_hdemo_sk", "c_first_shipto_date_sk", "c_first_sales_date_sk", "c_first_name", "c_last_name", "c_preferred_cust_flag", "c_email_address", "c_last_review_date"))

for i in range(100):
  userRecord = [fake.uuid4(), \
                fake.sha256(), \
                fake.words(1, c_current_cdemo_sk, True)[0], \
                fake.words(1, c_current_hdemo_sk, True)[0], \
                fake.date(), \
                fake.date(), \
                fake.first_name(), \
                fake.last_name(), \
                fake.words(1, ["Y", "N"], True)[0], \
                fake.email(), \
                fake.date()] 
  df1.loc[i] = [item for item in userRecord]
  
  
customer_data = spark.createDataFrame(df1)
display(customer_data)
