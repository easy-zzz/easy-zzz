---
дата создания: <% tp.file.creation_date() %>
дата изменений: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
Last modified date: <%+ tp.file.last_modified_date() %>
link: <% tp.file.cursor(1) %>
---


<% tp.user.my_script("Hello World!") %>
