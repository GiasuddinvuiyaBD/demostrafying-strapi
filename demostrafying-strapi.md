## Demostrafying Strapi Populate and filtering. 

`note : First we have to install qs`


populate relatives, First label request.
```js
const queryOb = {
    populate: ["profile_picture"]
}
```

populate and field select
```js
const queryOb = {
    populate: {
        profile_picture:
        {
            fields : ["name]
        }
    }
}
// it will provide us profile picture name.
```

populate and field select-2
```js
const queryOb = {
    populate: ["company", "company.misc_info"]
}
// it will provide us company data as well as company.misc_info which is under of the company.
```

populate deeply nested component
```js
const queryOb = {
   populate : {
    company : {
        misc_info:{
            on:{
                "company-secreats-info":{
                    populate : "*"
                }
            }
        }
    }
   }
}
// populate>company>misc_info>on:> "company-secreats-info">populate all 

//it means company's all secreats i want to get.
```

**Info :** Let's carray on. Where can i populate data ??

- Relations
- Components and Dynamix Zones
- Nested Relations.


**Filtering :** Sometimes our data can be complex, how to fineture our request to get the most relevant response possible? Filtering. Here's a few things about filtering in Strapi.

- A great place to start is our docs. Form there, you can learn about all the operators available for filtering
- In the Rest api, you can only filter when **find**ing data from core APIs
- Deep filters may cause performance issues. You might want to build a custom optimized query in this case
- Deep filtering is not available in DZs, and Media Fields.

## Example: 

Filter by top level attribute
```js
const queryOb = {
    filters:{
        happy: false
    }
}
// or
const queryOb = {
    filters:{
        happy: {
            $not: true
        }
    }
}

// form here it will filter data which happy are false.
```

Filter by relations
```js
const queryObj = {
    filters:{
        company:{
            big_tech: true
        }
    }
}

// insdie the company every data will show which are bit_tech equel to true
```

complex filtering
```js
const queryObj = {
    filters: {
        [
            $and: {
                happy : true
            },
            {
                company: {
                    big_tech : true
                }
            }
        ],
        profile_picture:{
            $not: null
        }
    }
}

// $and operator combine some particular field here i have added two field.

```

`console.log(qs.stringify(queryObj))`