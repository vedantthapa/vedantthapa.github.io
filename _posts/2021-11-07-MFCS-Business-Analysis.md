---
title: Mahindra First Choice Services (MCFS) Business Analysis
published: true
---

Mahindra First Choice Services (MFCS) is a company of Mahindra Group and is India’s leading chain of multi-brand car workshops with over 335+ workshops present in 267+ towns & 24 states. It has serviced over 10,50,000 cars. The company aims to establish countrywide network of over 400 workshops by March 2018.
Mahindra would now like to leverage the data that they have and address the key issues they have. Read along to know how you can help them improve their business.
The dataset consist of three aspects:

1. **Customer data**: where the details of the customer like the car owned, state and place of residence, order type, etc are present. Data dimension is of ​534000 Customer entries
2. **Invoice data**: ​where information related to customer visits and transactions are recorded, whether a customer as insurance claims, ​bifurcation of the amount paid, for what type of service did the customer came for, etc...
3. **Material Inventory**: where information related to what kind of service did the customer took and what kind of material was used to service, Labor information and the cost for the service, Plant and plant name where the customer took the service.

**Problem Statement-1**: Identifying the ownership pattern of cars throughout the country. This also captures the problem wherein information regarding the spending patterns can be identified.

- Mahindra First Choice Services will be benefited in multiple ways. Knowing the ownership pattern targeted marketing campaigns could be carried out. Knowing the spending patterns services could be suited to the particular spending pattern.

**Problem Statement-2**: Identify the various types of orders.

- This could potentially give information about how Mahindra First Choice needs to be prepared to tackle various seasonal cases.

**Problem Statement-3**: Revenue Analysis.

- This would help determine which streams of revenue are beneficial and improve marketing strategies.

<script type="text/javascript">
window.PlotlyConfig = {MathJaxConfig: 'local'};
if (window.MathJax) {MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}
if (typeof require !== 'undefined') {
require.undef("plotly");
requirejs.config({
    paths: {
        'plotly': ['https://cdn.plot.ly/plotly-2.4.2.min']
    }
});
require(['plotly'], function(Plotly) {
    window._Plotly = Plotly;
});
}
</script>

### [[Show me the Code]](https://github.com/vedantthapa/Mahindra-Business-Analysis)
---
<br>
Starting out with the project, a quick glance at the data will reveal that there are a number of columns that aren't relevant to the problem statement.


```python
display_all(invoice_df.head(3))
print(f'Shape of the raw DataFrame: {invoice_df.shape}')
```

<div class="table-wrapper" markdown="block">
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>Amt Rcvd From Custom</th>
      <th>Amt Rcvd From Ins Co</th>
      <th>Area / Locality</th>
      <th>CGST(14%)</th>
      <th>CGST(2.5%)</th>
      <th>CGST(6%)</th>
      <th>CGST(9%)</th>
      <th>CITY</th>
      <th>Cash /Cashless Type</th>
      <th>Claim No.</th>
      <th>Cust Type</th>
      <th>Customer No.</th>
      <th>District</th>
      <th>Expiry Date</th>
      <th>Gate Pass Date</th>
      <th>Gate Pass Time</th>
      <th>IGST(12%)</th>
      <th>IGST(18%)</th>
      <th>IGST(28%)</th>
      <th>IGST(5%)</th>
      <th>Insurance Company</th>
      <th>Invoice Date</th>
      <th>Invoice No</th>
      <th>Invoice Time</th>
      <th>Job Card No</th>
      <th>JobCard Date</th>
      <th>JobCard Time</th>
      <th>KMs Reading</th>
      <th>Labour Total</th>
      <th>Make</th>
      <th>Misc Total</th>
      <th>Model</th>
      <th>ODN No.</th>
      <th>OSL Total</th>
      <th>Order Type</th>
      <th>Outstanding Amt</th>
      <th>Parts Total</th>
      <th>Pin code</th>
      <th>Plant</th>
      <th>Plant Name1</th>
      <th>Policy no.</th>
      <th>Print Status</th>
      <th>Recovrbl Exp</th>
      <th>Regn No</th>
      <th>SGST/UGST(14%)</th>
      <th>SGST/UGST(2.5%)</th>
      <th>SGST/UGST(6%)</th>
      <th>SGST/UGST(9%)</th>
      <th>Service Advisor Name</th>
      <th>TDS amount</th>
      <th>Technician Name</th>
      <th>Total Amt Wtd Tax.</th>
      <th>Total CGST</th>
      <th>Total GST</th>
      <th>Total IGST</th>
      <th>Total SGST/UGST</th>
      <th>Total Value</th>
      <th>User ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>MAJIWADA</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>Thane</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Retail</td>
      <td>67849</td>
      <td>Maharashtra</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>00:00:00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>2015-01-02</td>
      <td>7005200002</td>
      <td>11:30:36</td>
      <td>168303</td>
      <td>2014-12-13</td>
      <td>14:29:43</td>
      <td>49317</td>
      <td>1203.14</td>
      <td>GENERAL MOTORS</td>
      <td>0.00</td>
      <td>SPARK</td>
      <td>7.005200e+09</td>
      <td>500.06</td>
      <td>Paid Service</td>
      <td>0.0</td>
      <td>2348.75</td>
      <td>400601</td>
      <td>BC01</td>
      <td>THANE</td>
      <td>NaN</td>
      <td>NO</td>
      <td>0.0</td>
      <td>KA19MA1291</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>RUPESH</td>
      <td>4051.95</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4051.95</td>
      <td>BC01FS1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>THNAE</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>THNAE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Retail</td>
      <td>84419</td>
      <td>Maharashtra</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>00:00:00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>2015-01-03</td>
      <td>7005200003</td>
      <td>10:07:32</td>
      <td>173997</td>
      <td>2015-01-02</td>
      <td>14:12:18</td>
      <td>78584</td>
      <td>804.26</td>
      <td>TATA MOTORS</td>
      <td>197.03</td>
      <td>INDICA</td>
      <td>7.005200e+09</td>
      <td>0.00</td>
      <td>SMC Value Package</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>400603</td>
      <td>BC01</td>
      <td>THANE</td>
      <td>NaN</td>
      <td>NO</td>
      <td>0.0</td>
      <td>MH43R3046</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>PRASHANT</td>
      <td>1001.29</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1001.29</td>
      <td>BC01SA2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>THANE</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>THANE[W]</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Retail</td>
      <td>81055</td>
      <td>Maharashtra</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>00:00:00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>2015-01-03</td>
      <td>7005200004</td>
      <td>11:12:57</td>
      <td>173889</td>
      <td>2015-01-02</td>
      <td>11:40:44</td>
      <td>33985</td>
      <td>180.19</td>
      <td>MARUTI SUZUKI</td>
      <td>0.00</td>
      <td>ZEN</td>
      <td>7.005200e+09</td>
      <td>0.00</td>
      <td>Running Repairs</td>
      <td>0.0</td>
      <td>52.95</td>
      <td>400607</td>
      <td>BC01</td>
      <td>THANE</td>
      <td>NaN</td>
      <td>NO</td>
      <td>0.0</td>
      <td>AP09AX0582</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>IMRAN</td>
      <td>233.14</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>233.14</td>
      <td>BC01SA2</td>
    </tr>
  </tbody>
</table>

</div>


    Shape of the raw DataFrame: (492314, 59)


Such columns can be dropped for the time being. We can add them later if needed.


```python
display_all(invoice_cleaned.head(3))
print(f'Shape of the cleaned DataFrame: {invoice_cleaned.shape}')
```


<div class="table-wrapper" markdown="block">
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CITY</th>
      <th>Cust Type</th>
      <th>Customer No.</th>
      <th>District</th>
      <th>Invoice No</th>
      <th>Job Card No</th>
      <th>KMs Reading</th>
      <th>Labour Total</th>
      <th>Make</th>
      <th>Misc Total</th>
      <th>Model</th>
      <th>OSL Total</th>
      <th>Order Type</th>
      <th>Outstanding Amt</th>
      <th>Parts Total</th>
      <th>Pin code</th>
      <th>Regn No</th>
      <th>Technician Name</th>
      <th>Total Amt Wtd Tax.</th>
      <th>User ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Thane</td>
      <td>Retail</td>
      <td>67849</td>
      <td>Maharashtra</td>
      <td>7005200002</td>
      <td>168303</td>
      <td>49317</td>
      <td>1203.14</td>
      <td>GENERAL MOTORS</td>
      <td>0.00</td>
      <td>SPARK</td>
      <td>500.06</td>
      <td>Paid Service</td>
      <td>0.0</td>
      <td>2348.75</td>
      <td>400601</td>
      <td>KA19MA1291</td>
      <td>RUPESH</td>
      <td>4051.95</td>
      <td>BC01FS1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>THNAE</td>
      <td>Retail</td>
      <td>84419</td>
      <td>Maharashtra</td>
      <td>7005200003</td>
      <td>173997</td>
      <td>78584</td>
      <td>804.26</td>
      <td>TATA MOTORS</td>
      <td>197.03</td>
      <td>INDICA</td>
      <td>0.00</td>
      <td>SMC Value Package</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>400603</td>
      <td>MH43R3046</td>
      <td>PRASHANT</td>
      <td>1001.29</td>
      <td>BC01SA2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>THANE[W]</td>
      <td>Retail</td>
      <td>81055</td>
      <td>Maharashtra</td>
      <td>7005200004</td>
      <td>173889</td>
      <td>33985</td>
      <td>180.19</td>
      <td>MARUTI SUZUKI</td>
      <td>0.00</td>
      <td>ZEN</td>
      <td>0.00</td>
      <td>Running Repairs</td>
      <td>0.0</td>
      <td>52.95</td>
      <td>400607</td>
      <td>AP09AX0582</td>
      <td>IMRAN</td>
      <td>233.14</td>
      <td>BC01SA2</td>
    </tr>
  </tbody>
</table>

</div>


    Shape of the cleaned DataFrame: (492314, 20)


In order to start with geolocation based analysis (Problem Statement - 1), the district column is necessary. However it requires cleaning because the values are inconsistent or erroneous at times. 

```python
invoice_cleaned.district.nunique()
```
    36



As a result, the district column is re-created using the pincodes provided so as to rectify the errors. **pgeocode** library is used to extract this information. However, some manual effort is still required to correct the remaining inconsistencies.


```python
invoice_cleaned.district.nunique()
```
    29


Now that these districts have been set, there are a few districts with relatively low frequencies. These districts have been reduced to a single value called `others`.


```python
other_states = invoice_cleaned.district.value_counts().index[11:]
other_states

    Index(['Kerala', 'Delhi', 'Chandigarh', 'Bihar', 'Himachal Pradesh',
           'Uttarakhand', 'Odisha', 'Puducherry', 'West Bengal', 'Chhattisgarh',
           'Dadra and Nagar Haveli and Daman and Diu', 'Jharkhand', 'Assam', 'Goa',
           'Arunachal Pradesh', 'Jammu & Kashmir', 'Lakshadweep', 'Nagaland'],
          dtype='object')
```



```python
invoice_cleaned['district_grp'] = np.where(invoice_cleaned.district.isin(other_states), 'Others', invoice_cleaned.district)
```

Also, there are 28 unique values for `make` in the dataset.


```python
invoice_cleaned.make.nunique()
```
    28

These values can be clubbed into a 4 distinct categories:
- Hatchback
- SUV
- Utility
- Luxury
- Sedan


```python
invoice_cleaned['model_type'].value_counts()
```


    Hatchback    281333
    SUV           98766
    Sedan         95397
    Utility       14478
    Luxury         2340
    Name: model_type, dtype: int64



With this we are ready to approach our first problem statement!

---

## Ownership patterns

{% include post1-fig1.html %}

The plot above aids us in comprehending our customer base. Before charting, the data was filtered by the `cust type` column to only include retail customers, as the ownership pattern can only be identified when the consumer owns the automobile.

The majority of our consumers come from the states of Maharashtra and Tamil Nadu. This is most likely attributable to the fact that these states have more service plants. Hatchbacks are the most popular category in the country, followed by SUVs. Maruti Suzuki is the most popular car brand among our consumers. A luxury automobile is owned only by a small percentage of clients.

The above observations suggest that the majority of our customers are from the middle class.

## Order types and Service Times

We'll need some feature engineering before moving on to the next problem statement. The difference (in hours) between the columns `JobCardDateTime` - signifies the time when the automobile arrived for service, and `InvoiceDateTime` - shows the time when the invoice was created, is used to create a new column called `service time hrs`.

This new feature indicates the amount of time, in hours, taken to perform the service.


```python
invoice_cleaned['InvoiceDateTime'] = pd.to_datetime(invoice_df['Invoice Date']+' '+invoice_df['Invoice Time'])
invoice_cleaned['JobCardDateTime'] = pd.to_datetime(invoice_df['JobCard Date']+' '+invoice_df['JobCard Time'])
```


```python
invoice_cleaned['service_time'] = invoice_cleaned['InvoiceDateTime'] - invoice_cleaned['JobCardDateTime']
invoice_cleaned["service_time_hrs"]=invoice_cleaned["service_time"]/np.timedelta64(1, 'h')
```

To determine the frequency and average service time, the above figure was created by grouping on the `order type` column and getting the average and count of the `service_time_hrs` column. To decrease the impact of outliers, the median was utilised to calculate the average.

{% include post1-fig2.html %}

After the above-mentioned aggregations, the plot reveals that a substantial percentage of our customer population (about 80%) visits our plant for running repairs and paid services. Running repairs often take roughly 6 hours to complete, whereas paid services typically take a day to complete. Accidental repairs take a long time to complete, which might be correlated to the magnitude of the damage or the availability of parts.

We can probably reduce the service times by knowing the nature of the visit beforehand and stocking up on the parts accordingly.

Let's analyze whether location plays a role in the time taken to complete a service.
    
![jpeg](../assets/post1/service-time-make-state-fig3.jpeg)
    
 Considering Maruti Suzuki, the most frequent car across states, we observe that the average service time in Telangana is relatively high. The second most popular brand - Mahindra & Mahindra, usually takes a day on average to complete the service.

It would be interesting to check if there is a seasonal trend in the number of incoming customers.
    
![jpeg](../assets/post1/orders-month-fig4.jpeg)

The heatmap above displays the various sorts of orders that have been received over the months. Over the years, we've seen that the majority of mechanical orders occur around January and August. Customers visiting a factory for paid service or running repairs, the two most typical forms of orders, do not follow a seasonal pattern.

Since there's no seasonal trend in the orders received, MFCS can stock up their inventory with common parts like oil and air filters for most popular car brands in order to reduce their service times.

Let's have a look at the customer arrive times over the dataset at a particular day. These arrival times are calculated based on the `JobCardDateTime` column.
    
![jpeg](../assets/post1/arrival-times-fig5.jpeg)

The majority of consumers arrive between 9 a.m. and 12 p.m. After 12 p.m., there is a downward tendency. This may assist MFCS in organising their labour force so that customers receive prompt help during peak hours.

## Revenue

Let's have a look at the revenue generated over the years and it's respective streams. We will also look at Parts-to-Labour ratio which is the ratio of labor sales to parts sold. The parts-to-labor ratio provides insight into how much a company's revenue is derived from services performed and how much depends on selling parts. MFCS managers can use parts-to-labor ratio to make informed decisions on how much to charge for labor and parts.

![jpeg](../assets/post1/bump-fig6.jpeg)

The graph above depicts how revenue has evolved over the years. We only look at the top six states (MH, TN, KA, RJ, TL, UP) because they contribute the most to overall revenue.

Overall, even though Maharashtra lost first place to Tamil Nadu in 2015, the state's revenue continues to rise. Many rankings shift after 2014, with Uttar Pradesh, which was ranked third in 2014, falling to last place by 2016. Rajasthan's revenue increased dramatically in 2016, owing to the opening of new factories by MFCS the previous year.

Parts-to-labor ratio is equal to parts sales divided by labor sales. For example, if an auto repair shop sells \$80,000 in parts during a certain month and charges customers \$100,000 for labor performed during that month, its parts-to-labor ratio for the month is 80,000 divided by 100,000, or 0.8. This means that for every dollar of labor sales that the company makes, it sells 80 cents worth of parts.

According to Bob O'Connor of Motor Magazine, a parts-to-labor ratio in the range of 0.8 to 1 is considered normal for the auto repair industry. If the parts-to-labor ratio exceeds 1, it means parts sales account for a greater proportion of total revenue than labor sales, which indicates that a shop is charging too little for labor or too much for parts.
    
![jpeg](../assets/post1/ratio-make-fig7.jpeg)

We can see from the diagram above that MFCS is charging too much for parts and too little for labour on majority of the automobiles. 

Given that our dataset consists primarily of labor-intensive running repairs and paid services, and that the majority of the automobiles are from the economical group (Maruti Suzuki, Mahindra & Mahindra, and so on), MFCS can strive to balance this ratio in order to maximise their profit margins.

Finally let's have a look at different sources of customers

![jpeg](../assets/post1/origin-customer-fig8.jpeg)

The origin of MFCS's client population can be seen in this graph. As can be observed, referrals account for about half of the total clients. The remaining 50% of clients come via marketing techniques such as hosting camps/workshops or placing ads in newspapers, television, and other media.

Knowing this, MFCS can improve its profit margins by enhancing its referral policies, lowering advertising expenditures in the process.
