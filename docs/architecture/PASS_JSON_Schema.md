# `pass.json` Configuration Schema

The `pass.json` file lives at the root of the ASP.NET Core project. It acts as the "Project Memory." If it does not exist, PASS creates it during the first scaffold. Every subsequent scaffold reads this file to maintain consistency.

## Example `pass.json`

```json
{
  "passVersion": "1.0",
  "projectSettings": {
    "framework": "net8.0",
    "architecture": "MVC"
  },
  "ui": {
    "theme": "Bootstrap5",
    "darkMode": true,
    "layout": "SidebarLayout",
    "gridComponent": "Syncfusion",
    "modalEditing": true
  },
  "data": {
    "pagination": true,
    "pageSize": 10,
    "globalSearch": true,
    "columnSearch": true,
    "sorting": true
  },
  "codeGeneration": {
    "validation": "FluentValidation",
    "auditTrail": true,
    "softDelete": true,
    "ajaxCrud": true
  },
  "security": {
    "authorization": "RoleBased",
    "antiForgery": true
  }
}
