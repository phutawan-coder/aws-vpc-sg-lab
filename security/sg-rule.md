## Security Groups

### sg-app
- Inbound:
  - SSH (22) from My IP
- Outbound:
  - All traffic

### sg-db
- Inbound:
  - SSH (22) from sg-app
  - DB port (3306) from sg-app
- Outbound:
  - All traffic

