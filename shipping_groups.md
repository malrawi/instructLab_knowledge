# What are shipping groups
A shipping group is way to logically group carrier services that meet a certain fulfillment criteria, a delivery promise, or share the main features, such as cost and/or Service Level Agreement (SLA).
Shipping groups can be thought of as a shipping option that is available to shoppers.

You can associate a maximum number of transit days to a shipping group to give guidelines about which carrier services can be included. You must configure the shipping group and 
associate at least one carrier service before the shipping group can be considered for Promising Calculations by the Calculate item delivery date and Calculate shipment assignments APIs.

You can pass the desired shipping group to calculation APIs (EDD & CCA) if the delivery method is SHP. 

Here are some examples of possible shipping groups:
 * STANDARD: Free shipping, with 7 maximum number of transit days, with possible carrier services: USPS_Ground, FedEx_Ground, and UPS_Ground.
 * EXPRESS: Paid shipping, with 3 maximum number of transit days, with possible carrier services: USPS_Air and UPS_Ground.
 * PREMIUM: Paid shipping, with 1 maximum number of transit days, with possible carrier services: FedEx_Express, and UPS_Express.

## How to create a shipping group
You can create a shipping group by invoking the Define shipping group API. You can invoke this API by using curl command, or using any HTTP REST clients, such as POSTMAN.
You need to specify the id for the created shipping group, maximum number of transit days, and a list of carrier services that belong to the shipping group. Here is an example:
```shell
curl --request PUT --url https://api.watsoncommerce.ibm.com/promising/REPLACE_TENANTID/v1/configuration/shippingGroups/ECONN \
  --header "Authorization: Bearer REPLACE_BEARER_TOKEN" \
  --header "accept: application/json" \
  --header "content-type: application/json" \
  --data '{
    "shippingGroup": {
      "shippingGroupId": "ECONN",
      "shippingGroupName": "ECONN Shipping",
      "maxShippingDays": 2,
      "carrierServices": [
        "USPS_Ground", "FedEx_Ground"
      ]
    }
  }'
```

### Notes:
* shippingGroupId: is the shipping group id, which should also be stamped in the URL. In the example above, ECONN is the shipping group id.
* shippingGroupName: is a descriptive name for your shipping group
* maxShippingDays: that is the maximum number of transit days. In other words, the shipping group's Service Level Agreement (SLA).
* carrierServices: is an array of strings that represent carrier service. In the example above, we listed USPS_Ground and FedEx_Ground. Note that the listed carrier services transit time should not exceed the value specified by maxShippingDays

## How to update a shipping group
You can use the Define shipping group API, which you would normally use to create a shipping group, except that you will need to pass the id of the shipping group you wish to 
update. Here is an example of how we can use the curl command to update ECONN shipping group to add UPS_Ground to the list of carrier services and to update the maximum shipping days:
```shell
curl --request PUT --url https://api.watsoncommerce.ibm.com/promising/REPLACE_TENANTID/v1/configuration/shippingGroups/ECONN \
  --header "Authorization: Bearer REPLACE_BEARER_TOKEN" \
  --header "accept: application/json" \
  --header "content-type: application/json" \
  --data '{
    "shippingGroup": {
      "shippingGroupId": "ECONN",
      "shippingGroupName": "ECONN Shipping",
      "maxShippingDays": 8,
      "carrierServices": [
        "USPS_Ground", "FedEx_Ground", "USPS_Ground"
      ]
    }
  }'
```




