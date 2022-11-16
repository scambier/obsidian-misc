# Mastodon

## Get your Mastodon bookmarks in Obsidian

> Required plugin: Dataview, with JavaScript enabled.

### 1) Create an application in Mastodon

Go into Settings > Development > New application

Give it a name, and check (at least) "read:bookmarks". Uncheck the "write" and "follow" scopes to avoid accidents

![image](https://user-images.githubusercontent.com/3216752/202004644-50561363-6ba8-43e3-aa8c-157c3f79fe34.png)

### 2) Get your access token

Once created, open the settings of your new application, and retrieve the access token. **Be careful to not share it!**

![image](https://user-images.githubusercontent.com/3216752/202004890-a529f1ca-9a94-4d85-b739-0fbfcd32119c.png)

### 3) Create the DataviewJS query

Replace `YOUR_TOKEN_HERE` with your actual token in the first line.  
Also replace `https://hachyderm.io` with your instance domain, in the second line.

~~~
```dataviewjs
const Authorization = "Bearer YOUR_TOKEN_HERE";
const url = "https://hachyderm.io/api/v1/bookmarks";
fetch(url, { headers: { Authorization } })
  .then((res) => res.json())
  .then((json) => {
    const data = dv
      .array(json)
      .sort((o) => o.created_at, "desc")
      .map((item) => [
        `<a href="${item.account.url}">${item.account.display_name}</a>`,
        `<div style="display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical">${item.content}</div>`,
        `<a href="${item.url}">🔗</a>`,
      ]);
    dv.table(["From", "Toot", "Link"], data);
  });
```
~~~
![image](https://user-images.githubusercontent.com/3216752/202005723-79404b7f-756d-4254-904d-2a7b2c41b8f7.png)

### 4) Layout tip

If you use the _Minimal_ theme and the _Style Settings_ plugin, you can uncheck "Trim Dataview columns" for a better look

![image](https://user-images.githubusercontent.com/3216752/202014594-f6c2938e-ba60-4d68-8e1b-12448fca4b15.png)
