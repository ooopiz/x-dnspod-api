# dnspod-api
A dnspod api for nodejs.

## Features

- multiple-instance.

- promise.

- use login token replace user & password auth.

- server for dnspod.com or dnspod.cn.


## Useage

### BIN
```sh
dnspod-api --token 'xxxxx,xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' --action 'Domain.List'
```

or  

```sh
dnspod-api -u 'https://api.dnspod.com' -t 'xxxxx,xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' -a 'Record.List' -p '{"domain": "hateip.com", "sub_domain": "@"}'
```

please replace `$` with `\$` in token string.

### API Example

```js

// new dnspodApi instance
var dnspodApi =  new DnspodApi({
    url : 'https://dnsapi.cn', // https://dnsapi.cn (default) | https://api.dnspod.com
    token : 'xxxxx,xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' // your login token, you can find how to get token in then bottom.
});

// do actions
dnspodApi.do({
    action : 'Domain.List'
})
.then(
    // success
    function(domainListData){
        
        console.log('Domain List: ', domainListData);
        
        return dnspodApi.do({
            action : 'Record.List',
            params : {
                domain : 'your-domain.com',
                sub_domain : '@'
            }
        });

    },
    // error
    function(error) {
        console.log(error);
    }
)
.then(
    function(recordListData){
        console.log('Record List: ', recordListData);
    },
    // error
    function(error) {
        console.log(error);
    }
)
//.then ....
```


## DNSPOD API documents
> Dnspod.cn : https://www.dnspod.cn/docs  
> Dnspod.com : https://www.dnspod.com/docs

## How to get token
> Dnspod.cn : https://support.dnspod.cn/Kb/showarticle/tsid/227  
> Dnspod.com : https://www.dnspod.com/docs/info.html#get-the-user-token