---
дата создания: <% tp.file.creation_date() %>
дата изменений: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
link: <% tp.file.cursor(${order2 ?? ""}) %>
---


