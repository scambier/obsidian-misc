<%*
let date = moment(tp.file.title,'YYYY-MM-DD').format("YYYY-MM-DD")
-%>
# <% date %>

- <% tp.file.cursor() %>

## TODO

- [ ]

## Due this day

```tasks  
not done
(due <% date %>) OR (due before <% date %>)
```

## Done this day

```tasks  
done <% date %>
```
