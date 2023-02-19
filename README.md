# Creating JSON in D3

This is a very simply set of programs to create json in Rocket's multivalue database D3.

**Warning: You cannot use '[' or '{' as the starting character in a value.**

## Installation

Download the files, compile them and then catalog them.

## Example

This is the code to create some json. You can create key value pairs, arrays and objects.

```
*
    BUFFER = ''
*
* ADD REGULAR KEYS
*
    CALL JSON.ADD(BUFFER,'part','ASD-123')
    CALL JSON.ADD(BUFFER,'description','Some' : "'" : 's Part, 55LB, 800LB"')
    CALL JSON.ADD(BUFFER,'listPrice','912.00')
    CALL JSON.ADD(BUFFER,'dealerCost','712.00')
    CALL JSON.ADD(BUFFER,'percent30','643.50')
    CALL JSON.ADD(BUFFER,'percent10','511.81')
    CALL JSON.ADD(BUFFER,'shipBy','T')
*
* ADD AN ARRAY OF OBJECTS
*
    ORDER.ARRAY = ''
*
    FOR I = 1 TO 2
        ORDER.BUFFER = ''
*
        CALL JSON.ADD(ORDER.BUFFER,'order','315215')
        CALL JSON.ADD(ORDER.BUFFER,'qty','1')
        CALL JSON.ADD(ORDER.BUFFER,'customer','')
        CALL JSON.ADD(ORDER.BUFFER,'customerName','')
        CALL JSON.ADD(ORDER.BUFFER,'po','')
        CALL JSON.ADD(ORDER.BUFFER,'requiredDate','')
*
        CALL JSON.CREATE.OBJECT(ORDER.JSON,ORDER.BUFFER)

        ORDER.ARRAY<-1> = ORDER.JSON
    NEXT I
*
    CALL JSON.CREATE.ARRAY(JSON.ARRAY,ORDER.ARRAY)
    CALL JSON.ADD(BUFFER,'orders',JSON.ARRAY)
*
* ADD AN OBJECT AS A VALUE
*
    CUSTOMER = ''
*
    CALL JSON.ADD(CUSTOMER,'id','123')
    CALL JSON.ADD(CUSTOMER,'name','The Design Company')
    CALL JSON.ADD(CUSTOMER,'orders',JSON.ARRAY)
    CALL JSON.CREATE.OBJECT(JSON,CUSTOMER)
*
    CALL JSON.ADD(BUFFER,'customer',JSON)
*
* CREATE FINAL JSON
*
    CALL JSON.CREATE.OBJECT(JSON,BUFFER)
*
    PRINT JSON
*
    STOP
*
* END OF PROGRAM
*
    END
*
```

This outputs the following:

``` json
{
   "part":"ASD-123",
   "description":"Some's Part, 55LB, 800LB\"",
   "listPrice":912.00,
   "dealerCost":712.00,
   "percent30":643.50,
   "percent10":511.81,
   "shipBy":"T",
   "orders":[
      {
         "order":315215,
         "qty":1,
         "customer":"",
         "customerName":"",
         "po":"",
         "requiredDate":""
      },
      {
         "order":315215,
         "qty":1,
         "customer":"",
         "customerName":"",
         "po":"",
         "requiredDate":""
      }
   ],
   "customer":{
      "id":123,
      "name":"The Design Company",
      "orders":[
         {
            "order":315215,
            "qty":1,
            "customer":"",
            "customerName":"",
            "po":"",
            "requiredDate":""
         },
         {
            "order":315215,
            "qty":1,
            "customer":"",
            "customerName":"",
            "po":"",
            "requiredDate":""
         }
      ]
   }
}
```

## Blog Posts

https://nivethan.dev/devlog/d3-json-creation.html

https://nivethan.dev/devlog/d3-json-creation---the-how.html


