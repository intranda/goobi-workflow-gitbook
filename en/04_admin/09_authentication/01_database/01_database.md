# Authentication via the database

With database authentication, users are managed entirely by Goobi workflow itself. The user name and password are stored in the Goobi database. Within the database, only a hash (`sha256` & `salt`) of the password is stored and compared with the user password entered at login.