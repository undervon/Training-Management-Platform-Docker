# Training-Management-Platform-Docker

### authentication.authorization.jwt (microservice)

#### http://localhost:8090/swagger-ui/index.html -> URL to access Swagger

##### Commands until integrate Liquibase to Docker (right now is integrated)

<ul>
	<li>psql -U postgres -> connecting to postgres using CLI</li>
	<li>\l | \list -> show DB-s</li>
	<li>\c trainingManagementPlatform -> connecting to specific DB</li>
	<li>\dt -> show tables</li>
</ul>

##### After connecting, paste this:
~~~
INSERT INTO ROLES(ROLE_VALUE)
VALUES ('ADMIN');

INSERT INTO ROLES(ROLE_VALUE)
VALUES ('MANAGER');

INSERT INTO ROLES(ROLE_VALUE)
VALUES ('EMPLOYEE');

INSERT INTO MANAGERS(EMAIL)
VALUES ('manager@manager.com');

INSERT INTO MANAGERS(EMAIL)
VALUES ('manager.generic@manager.com');

INSERT INTO MANAGERS(EMAIL)
VALUES ('silviu.butnaru@student.tuiasi.ro');

INSERT INTO MANAGERS(EMAIL)
VALUES ('marian-ilie.butnaru@student.tuiasi.ro');

INSERT INTO MANAGERS(EMAIL)
VALUES ('alexandra.stefan@student.tuiasi.ro');

INSERT INTO MANAGERS(EMAIL)
VALUES ('alberto-ionut.toscariu@student.tuiasi.ro');

-- pass: admin<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('ADMIN', 'admin@admin.com', 'UIC0', 'admin', 'admin',
        (SELECT id_manager FROM MANAGERS WHERE email = 'manager@manager.com'),
        '$2a$10$LT7B3Tc47NuzcpZDEvPt5.ctHrHbM/AECWTgn53EgVOkHwNy6kV4C', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/admin-icon.png'));

-- pass: silviu<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('HMI', 'silviu.butnaru@student.tuiasi.ro', 'UIC1', 'Silviu', 'Butnaru',
        (SELECT id_manager FROM MANAGERS WHERE email = 'manager@manager.com'),
        '$2a$10$8ZDaoPmScOgEclTEUMh/Ku6njvMX3ae.qiQKNax9YKPsd7rqa2irO', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/manager-icon.png'));

-- pass: marian-ilie<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('VNI', 'marian-ilie.butnaru@student.tuiasi.ro', 'UIC2', 'Marian-Ilie', 'Butnaru',
        (SELECT id_manager FROM MANAGERS WHERE email = 'manager@manager.com'),
        '$2a$10$I8W/6hos1D1XBjXWD3uEBu9CKjn8Gf95mRki1bjqafEVAdCqxGdFy', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/manager-icon.png'));

-- pass: alexandra<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('HMI', 'alexandra.stefan@student.tuiasi.ro', 'UIC3', 'Alexandra', 'Stefan',
        (SELECT id_manager FROM MANAGERS WHERE email = 'silviu.butnaru@student.tuiasi.ro'),
        '$2a$10$LfggPragOiLHiLBBf3wSAe6//absugtgc86Cxr9Wl.mMG/RaXY19C', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/manager-icon.png'));

-- pass: alberto-ionut<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('VNI', 'alberto-ionut.toscariu@student.tuiasi.ro', 'UIC4', 'Alberto-Ionut', 'Toscariu',
        (SELECT id_manager FROM MANAGERS WHERE email = 'marian-ilie.butnaru@student.tuiasi.ro'),
        '$2a$10$PGIKEzrA35U077fFS8H1hu30ZOXGZCTrKtmpWu68hQKOJ0ehnpVO6', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/manager-icon.png'));

-- pass: andrei<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('HMI', 'andrei.petcu@student.tuiasi.ro', 'UIC5', 'Andrei', 'Petcu',
        (SELECT id_manager FROM MANAGERS WHERE email = 'alexandra.stefan@student.tuiasi.ro'),
        '$2a$10$D6rLx4u1tiSzbfJWC5kv4e6BoN34/AuWAGeYhpEqdBKfNOG9wzMO2', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/user-icon.png'));

-- pass: dan-claudiu<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('HMI', 'dan-claudiu.taga@student.tuiasi.ro', 'UIC6', 'Dan-Claudiu', 'Taga',
        (SELECT id_manager FROM MANAGERS WHERE email = 'alexandra.stefan@student.tuiasi.ro'),
        '$2a$10$m8sYIzF5QKLDb/pxnTZD4uoDGSXo1VVYA7.UnZ0SLzfIwpWykib0e', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/user-icon.png'));

-- pass: laurentiu-stefan<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('VNI', 'laurentiu-stefan.balauta@student.tuiasi.ro', 'UIC7', 'Laurentiu-Stefan', 'Balauta',
        (SELECT id_manager FROM MANAGERS WHERE email = 'alberto-ionut.toscariu@student.tuiasi.ro'),
        '$2a$10$OtbNdQlqR.oYoKh8xoNJh.xeXSprUDn3Bpp9HYH21b67oZKuQ9Yzi', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/user-icon.png'));

-- pass: mihai-adrian<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('VNI', 'mihai-adrian.mircea@student.tuiasi.ro', 'UIC8', 'Mihai-Adrian', 'Mircea',
        (SELECT id_manager FROM MANAGERS WHERE email = 'alberto-ionut.toscariu@student.tuiasi.ro'),
        '$2a$10$SZSFkqe5gnQ8da3aU/VCB.rXihpaYE.y0Hk8zOWbOdeduOqWiktdm', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/user-icon.png'));

-- pass: rares-petru<br>
INSERT INTO EMPLOYEES(DEPARTMENT, EMAIL, EMPLOYEE_NUMBER, FIRST_NAME, LAST_NAME, ID_MANAGER, PASSWORD, JOIN_DATE, IMAGE)
VALUES ('VNI', 'rares-petru.vanga@student.tuiasi.ro', 'UIC9', 'Rares-Petru', 'Vanga',
        (SELECT id_manager FROM MANAGERS WHERE email = 'alberto-ionut.toscariu@student.tuiasi.ro'),
        '$2a$10$TepbieCCQVS0EvxR3z/1luay4orkFprwoQFQeIlCDLxU9V3f8zhZC', CURRENT_TIMESTAMP,
        LO_IMPORT('/docker-entrypoint-initdb.d/user-icon.png'));

-- admin -> ADMIN<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'admin@admin.com'),
        (SELECT id_role FROM ROLES WHERE role_value = 'ADMIN'));

-- silviu -> MANAGER, EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'silviu.butnaru@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'MANAGER'));
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'silviu.butnaru@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));

-- marian-ilie -> MANAGER, EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'marian-ilie.butnaru@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'MANAGER'));
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'marian-ilie.butnaru@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));

-- alexandra -> MANAGER, EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'alexandra.stefan@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'MANAGER'));
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'alexandra.stefan@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));

-- alberto-ionut -> MANAGER, EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'alberto-ionut.toscariu@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'MANAGER'));
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'alberto-ionut.toscariu@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));

-- andrei: EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'andrei.petcu@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));

-- dan-claudiu: EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'dan-claudiu.taga@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));

-- laurentiu-stefan: EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'laurentiu-stefan.balauta@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));

-- mihai-adrian: EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'mihai-adrian.mircea@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));

-- rares-petru: EMPLOYEE<br>
INSERT INTO EMPLOYEES_ROLES(ID_EMPLOYEE, ID_ROLE)
VALUES ((SELECT id_employee FROM EMPLOYEES WHERE email = 'rares-petru.vanga@student.tuiasi.ro'),
        (SELECT id_role FROM ROLES WHERE role_value = 'EMPLOYEE'));
~~~
