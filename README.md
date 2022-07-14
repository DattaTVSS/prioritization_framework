# prioritization_framework
To use the saved scripts in ES and prioritise the search order for an entity


# Impact of this for Invoices Flow
1. Improving the customer experience for Retailer to process them, which would eventually result in increase of Vendor NPS
2. Supply Chain Financing
3. Quicker unblocking of Inventory from WH for returns


# Approach
The script of ES would use fields and by creating a metric for each attribute so that all of them would have same range.
The attributes and corresponding metrics used for Invoice prioritization.

| Attribute | Metric                      | Usage/Impact |
| --------- | ------                      | ------------ |
| due_date  | if <0, 1/1-e^-x, else 1/x+1 | Every vendor wants the payments to be done on due, this is very critical to vendor NPS as well |
| aging     | 1/x+1                       | One shouldn't keep the invoice unprocesssed for long as the WH Inventory movement would be blocked |
| SCF       | 0.1 if false, else 1        | As an organisation, processing SCF invoices earlier would help |
| items     | 1/x+1                       | Retailer wants to process invoices with lesser items first as it increases throughput |
| Category  | Based on category map, the priority is assigned | HyperLocal would be a priority, similarly each category ranking can be defined by user |

The score of each document can be computed using weighted mean of these metrics where one can compute weights from historical data.

The advantage of this approach is that even after adding filters, the prioritization still works


# Future Scope
The scripts once saved in the ES, the application built would have config for script name to be used, based on which the search would be prioritized now using this script.  
