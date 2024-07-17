# What are shipping groups
It is important to understand that the term shipping groups is not related to grouping shipments, nor consolidating shipments.
In IBM Sterling Intelligent Promising, the term shipping group refers to logically grouping carrier services that share certain 
fulfillment criteria or characteristics, such as cost and/or Service Level Agreement (SLA).

A key component of a shipping group is the list of carrier services that make up the shipping group. Carrier services are 
also referred to as "services". A carrier such as FedEx, USPS, etc., have different services such as ground, express, and same-day.

You can associate a maximum number of transit days to a shipping group to give guidelines about which carrier services can be included. You must configure the shipping group and
associate at least one carrier service before the shipping group can be considered for Promising Calculations by the Calculate item delivery date and Calculate shipment assignments APIs.

For instance the following carrier services, or services,: FedEx's ground, USPS ground, UPS ground can be grouped togather
in one shipping group named STANDARD. These services happen to have the same SLA (8 days), and they are the cheapest.

Here are more examples of possible shipping groups:
* STANDARD: Free shipping, with 7 maximum number of transit days, with "ground" carrier services, or services, from USPS, FedEx, and UPS.
* EXPRESS: Paid shipping, with 3 maximum number of transit days, with "express" carrier services, or services from different carriers.
* PREMIUM: Paid shipping, with 1 maximum number of transit days, with "same-day" services from different carriers, such as FedEx and UPS.

## Where to use shipping groups 
Once a shipping group is created, you can pass to Calculation APIs (EDD & CCA), when the delivery method is SHP.

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

The following attributes are mandatory: carrierServices, maxShippingDays, shippingGroupName:
* shippingGroupName: is a descriptive name for your shipping group
* maxShippingDays: that is the maximum number of transit days. In other words, the shipping group's Service Level Agreement (SLA).
* carrierServices: is a list of services. In the example above, we listed USPS_Ground and FedEx_Ground. Note that the listed carrier services transit time should not exceed the value specified by maxShippingDays

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




