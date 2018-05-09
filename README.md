experimental kivitendo_docker
================

Docker Build for Kivitendo a erp solution for small businesses.
 - Ubuntu:14.04
 - Postgresql 9.3
 - Kivitendo 3.5.2
 - Midnight Commander
 - phppgadmin



# Start the app

Browser: http://"ipadress":"port"/kivitendo-erp/



# ToDo´s
- Export old DB: pg_dumpall -h localhost -U docker > dump.sql
- Import old DB: psql -h localhost -U docker < dump.sql
- Import Templates Files
- Configuration of Taskserver for autostartup  (see manual)
- Adaptation kivitendo-config
