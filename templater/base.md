---
дата создания: <% tp.file.creation_date() %>
дата изменений: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
link: <% tptp.file.cursor(${order2 ?? ""}) %>
---


