# Restish

a generic cli for APIs


```
# List the product types
~/go/bin/restish http://admin:password@127.0.0.1:8080/api/v2/product_types/

# Create a bunch of departments
~/go/bin/restish post http://admin:password@127.0.0.1:8080/api/v2/product_types/ name: Manufacturing
~/go/bin/restish post http://admin:password@127.0.0.1:8080/api/v2/product_types/ name: Accounting
~/go/bin/restish post http://admin:password@127.0.0.1:8080/api/v2/product_types/ name: Marketing
~/go/bin/restish post http://admin:password@127.0.0.1:8080/api/v2/product_types/ name: Customer Service

# Create a bunch of projects

# Get the product type id
PRODUCT_TYPE_ID=`curl http://admin:password@127.0.0.1:8080/api/v2/product_types/ | jq '.results[] | select (.name=="Accounting") | .id'`
~/go/bin/restish post http://admin:password@127.0.0.1:8080/api/v2/products/ name: TubiTax, description: tax software, prod_type: $PRODUCT_TYPE_ID

~/go/bin/restish post http://admin:password@127.0.0.1:8080/api/v2/products/ name: Ledgerbooks, description: corporate money tracking software, prod_type: $PRODUCT_TYPE_ID

# Add projects to the Customer Service department
PRODUCT_TYPE_ID=`curl http://admin:password@127.0.0.1:8080/api/v2/product_types/ | jq '.results[] | select (.name=="Customer Service") | .id'`
~/go/bin/restish post http://admin:password@127.0.0.1:8080/api/v2/products/ name: bugtrac, description: ticketing system, prod_type: $PRODUCT_TYPE_ID

# Add an engagement or two
# get the product id
PRODUCT_ID=`curl http://admin:password@127.0.0.1:8080/api/v2/products/ | jq '.results[] | select (.name=="bugtrac") | .id'`

~/go/bin/restish post http://admin:password@127.0.0.1:8080/api/v2/engagements/ product: $PRODUCT_ID, target_start: `date +%Y-%m-%d`, target_end: `date +%Y-%m-%d -d +7day`

curl -X POST "http://localhost:8080/api/v2/import-scan/" -u admin:password -F "engagement=1" -F "scan_type=Anchore Engine Scan" -F "file=@debian_7.json;type=application/json"
```
