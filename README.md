
CREATE DATABASE HcHs
ON PRIMARY
(
NAME=hospi_dat,
FILENAME='C:\HCHR\HcHs.mdf',
SIZE=6,
MAXSIZE=12,
FILEGROWTH=1
)
LOG ON
(
NAME=hospi_log,
FILENAME='C:\HCHR\HcHs.ldf',
SIZE=3,
MAXSIZE=5,
FILEGROWTH=1
)
Go
Use HcHs
Go

CREATE TABLE Servicio (
        codigoPrestacion INTEGER NOT NULL IDENTITY (1234,1),
		nombre VARCHAR(40) NOT NULL,
		disponibilidad CHAR(2) NOT NULL,
		codigoRenaes INTEGER NOT NULL
	)
GO

CREATE TABLE ESTABLECIMIENTO_SALUD_DESTINO (
		codigoRenaes INTEGER NOT NULL
	)
GO

CREATE TABLE ESTABLECIMIENTO_SALUD_ORIGEN (
		codigoRenaes INTEGER NOT NULL
	)
GO

CREATE TABLE RECIEN_NACIDO (
		PACIENTE_ID INTEGER NOT NULL,
		edadGestacional INTEGER NOT NULL,
		corteTardioCordon CHAR(1) NOT NULL

		
	)
GO

CREATE TABLE PACIENTE_FEMENINO (
		PACIENTE_ID INTEGER NOT NULL,
		saludMaterna CHAR(15) NULL,
		alturaUterina INTEGER NULL,
		edadGestacional INTEGER NULL,
		fechaProbableParto DATETIME NULL,
		partoVertical CHAR(2) NULL
	)
GO

CREATE TABLE Adolescente (
		PACIENTE_ID INTEGER NOT NULL,
		perimetroAbdominal VARCHAR(10) NULL,
		IMC VARCHAR(10) NULL,
	)
GO

CREATE TABLE Paciente (
		PACIENTE_ID INTEGER NOT NULL IDENTITY (5832145,1),
		nombres VARCHAR(50) NOT NULL,
		apellidos VARCHAR(50) NOT NULL,
		edad INTEGER NOT NULL,
		sexo CHAR(1) NOT NULL,
		fechaNacimiento DATETIME NOT NULL,
		correoElectronico VARCHAR(30) NULL,
		dni INTEGER NOT NULL,
		codigoSIS INTEGER NOT NULL,
		estadoSeguro VARCHAR(10) NOT NULL,
		etnia VARCHAR(15) NOT NULL,
		numeroHistoriaClinica INTEGER NOT NULL
	)
GO

CREATE TABLE ADMISIONISTA_HOSPITAL (
		codAdmiD INTEGER NOT NULL IDENTITY (1476,1),
		nombres VARCHAR(30) NOT NULL,
		apellidos VARCHAR(50) NOT NULL,
		codigoRenaes INTEGER NOT NULL,
		turnoTrabajo VARCHAR(10)
	)
GO



CREATE TABLE Cita (
		numeroCita INTEGER NOT NULL IDENTITY (13453,1),
		nombreServicio VARCHAR(40) NOT NULL,
		hora time NOT NULL,
		fechaIngreso DATE NOT NULL,
		fechaAlta DATE NULL,
		destinoAsegurado VARCHAR(30) NOT NULL,
		codigoEspecialista INTEGER NOT NULL,
		codAdmior INTEGER NULL,
		codAdmiD INTEGER NOT NULL,
		PACIENTE_ID INTEGER NOT NULL
	)
GO

CREATE TABLE Especialista (
		codigoEspecialista INTEGER NOT NULL IDENTITY (10143,1),
		DEPARTAMENTODEPARTAMENTO_ID INTEGER NOT NULL,
		nombres VARCHAR(30) NOT NULL,
		apellidos VARCHAR(50) NOT NULL,
		edad INTEGER NOT NULL,
		numeroCelular VARCHAR(9) NOT NULL,
		direccion VARCHAR(100) NOT NULL,
		especialidad VARCHAR(30) NOT NULL,
		a??oContrato VARCHAR(4) NOT NULL,
		numeroColegiatura INTEGER NOT NULL,
		numeroRNE INTEGER NOT NULL,
	)
GO

CREATE TABLE Departamento (
		DEPARTAMENTO_ID INTEGER NOT NULL IDENTITY (101,1),
		nombreDepartamento VARCHAR(50) NOT NULL
	)
GO

CREATE TABLE PRODUCTO_FARMACEUTICO (
		codigoMedicamento INTEGER NOT NULL IDENTITY (1743921,1),
		nombre VARCHAR(40) NOT NULL,
		concentracion VARCHAR(10) NOT NULL,
		formaFarmaceutica VARCHAR(30) NOT NULL,
		numeroCita INTEGER NOT NULL
	)
GO

CREATE TABLE Vacuna (
		codigoVacuna INTEGER NOT NULL IDENTITY (8321,1),
		nombreVacuna VARCHAR(20) NOT NULL,
		numeroDosis INTEGER NOT NULL,
		numeroCita INTEGER NOT NULL
	)
GO

CREATE TABLE PRODUCTO_SANITARIO (
		codigoProductoSan INTEGER NOT NULL IDENTITY (1249641,1),
		nombre VARCHAR(30) NULL,
		presentacion VARCHAR(20) NULL,
		caracteristica VARCHAR(100) NULL,
		numeroCita INTEGER NOT NULL
	)
GO

CREATE TABLE Diagnostico (
		codigoDiagnostico INTEGER NOT NULL IDENTITY (158,1),
		afeccion VARCHAR(15) NOT NULL,
		tipoDiagnostico VARCHAR(10) NOT NULL,
		numeroCita INTEGER NOT NULL
	)
GO

CREATE TABLE ADMISIONISTA_HOSPITAL_ORIGEN (
		codAdmior INTEGER NOT NULL IDENTITY (1256,1),
		nombres VARCHAR(40) NOT NULL,
		apellidos VARCHAR(50) NOT NULL,
		turnoTrabajo VARCHAR(20) NOT NULL,
		codigoRenaes INTEGER NOT NULL
	)
GO

CREATE TABLE ESTABLECIMIENTO_SALUD (
		codigoRenaes INTEGER NOT NULL,
		nombreEstablecimiento VARCHAR(70) NOT NULL,
		distrito VARCHAR(70) NOT NULL
		
	)
GO

ALTER TABLE Servicio ADD CONSTRAINT Servicio_PK PRIMARY KEY
	(codigoPrestacion)
GO

ALTER TABLE ESTABLECIMIENTO_SALUD_DESTINO ADD CONSTRAINT ESTABLECIMIENTO_SALUD_DESTINO_PK PRIMARY KEY
	(codigoRenaes)
GO

ALTER TABLE ESTABLECIMIENTO_SALUD_ORIGEN ADD CONSTRAINT ESTABLECIMIENTO_SALUD_ORIGEN_PK PRIMARY KEY
	(codigoRenaes)
GO

ALTER TABLE RECIEN_NACIDO ADD CONSTRAINT RECIEN_NACIDO_PK PRIMARY KEY
	(PACIENTE_ID)
GO

ALTER TABLE PACIENTE_FEMENINO ADD CONSTRAINT PACIENTE_FEMENINO_PK PRIMARY KEY
	(PACIENTE_ID)
GO

ALTER TABLE Adolescente ADD CONSTRAINT Adolescente_PK PRIMARY KEY
	(PACIENTE_ID)
GO

ALTER TABLE Paciente ADD CONSTRAINT Paciente_PK PRIMARY KEY
	(PACIENTE_ID)
GO

ALTER TABLE ADMISIONISTA_HOSPITAL ADD CONSTRAINT ADMISIONISTA_HOSPITAL_PK PRIMARY KEY
	(codAdmiD)
GO

ALTER TABLE Cita ADD CONSTRAINT Cita_PK PRIMARY KEY
	(numeroCita)
GO

ALTER TABLE Especialista ADD CONSTRAINT Especialista_PK PRIMARY KEY
	(codigoEspecialista)
GO

ALTER TABLE Departamento ADD CONSTRAINT Departamento_PK PRIMARY KEY
	(DEPARTAMENTO_ID)
GO

ALTER TABLE PRODUCTO_FARMACEUTICO ADD CONSTRAINT PRODUCTO_FARMACEUTICO_PK PRIMARY KEY
	(codigoMedicamento)
GO

ALTER TABLE Vacuna ADD CONSTRAINT Vacuna_PK PRIMARY KEY
	(codigoVacuna)
GO

ALTER TABLE PRODUCTO_SANITARIO ADD CONSTRAINT PRODUCTO_SANITARIO_PK PRIMARY KEY
	(codigoProductoSan)
GO

ALTER TABLE Diagnostico ADD CONSTRAINT Diagnostico_PK PRIMARY KEY
	(codigoDiagnostico)
GO

ALTER TABLE ADMISIONISTA_HOSPITAL_ORIGEN ADD CONSTRAINT ADMISIONISTA_HOSPITAL_ORIGEN_PK PRIMARY KEY
	(codAdmior)
GO

ALTER TABLE ESTABLECIMIENTO_SALUD ADD CONSTRAINT ESTABLECIMIENTO_SALUD_PK PRIMARY KEY
	(codigoRenaes)
GO

ALTER TABLE Servicio ADD CONSTRAINT Servicio_ESTABLECIMIENTO_SALUD_DESTINO_FK FOREIGN KEY
	(codigoRenaes)
	REFERENCES ESTABLECIMIENTO_SALUD_DESTINO
	(codigoRenaes)
GO

ALTER TABLE ESTABLECIMIENTO_SALUD_DESTINO ADD CONSTRAINT ESTABLECIMIENTO_SALUD_DESTINO_ESTABLECIMIENTO_SALUD_FK FOREIGN KEY
	(codigoRenaes)
	REFERENCES ESTABLECIMIENTO_SALUD
	(codigoRenaes)
GO

ALTER TABLE ESTABLECIMIENTO_SALUD_ORIGEN ADD CONSTRAINT ESTABLECIMIENTO_SALUD_ORIGEN_ESTABLECIMIENTO_SALUD_FK FOREIGN KEY
	(codigoRenaes)
	REFERENCES ESTABLECIMIENTO_SALUD
	(codigoRenaes)
GO

ALTER TABLE RECIEN_NACIDO ADD CONSTRAINT RECIEN_NACIDO_Paciente_FK FOREIGN KEY
	(PACIENTE_ID)
	REFERENCES Paciente
	(PACIENTE_ID)
GO

ALTER TABLE PACIENTE_FEMENINO ADD CONSTRAINT PACIENTE_FEMENINO_Paciente_FK FOREIGN KEY
	(PACIENTE_ID)
	REFERENCES Paciente
	(PACIENTE_ID)
GO

ALTER TABLE Adolescente ADD CONSTRAINT Adolescente_Paciente_FK FOREIGN KEY
	(PACIENTE_ID)
	REFERENCES Paciente
	(PACIENTE_ID)
GO

ALTER TABLE ADMISIONISTA_HOSPITAL ADD CONSTRAINT ADMISIONISTA_HOSPITAL_ESTABLECIMIENTO_SALUD_DESTINO_FK FOREIGN KEY
	(codigoRenaes)
	REFERENCES ESTABLECIMIENTO_SALUD_DESTINO
	(codigoRenaes)
GO

ALTER TABLE Cita ADD CONSTRAINT Cita_Especialista_FK FOREIGN KEY
	(codigoEspecialista)
	REFERENCES Especialista
	(codigoEspecialista)
GO

ALTER TABLE Cita ADD CONSTRAINT Cita_ADMISIONISTA_HOSPITAL_ORIGEN_FK FOREIGN KEY
	(codAdmior)
	REFERENCES ADMISIONISTA_HOSPITAL_ORIGEN
	(codAdmior)
GO

ALTER TABLE Cita ADD CONSTRAINT Cita_ADMISIONISTA_HOSPITAL_FK FOREIGN KEY
	(codAdmiD)
	REFERENCES ADMISIONISTA_HOSPITAL
	(codAdmiD)
GO

ALTER TABLE Cita ADD CONSTRAINT Cita_Paciente_FK FOREIGN KEY
	(PACIENTE_ID)
	REFERENCES Paciente
	(PACIENTE_ID)
GO

ALTER TABLE Especialista ADD CONSTRAINT Especialista_Departamento_FK FOREIGN KEY
	(DEPARTAMENTODEPARTAMENTO_ID)
	REFERENCES Departamento
	(DEPARTAMENTO_ID)
GO

ALTER TABLE PRODUCTO_FARMACEUTICO ADD CONSTRAINT PRODUCTO_FARMACEUTICO_Cita_FK FOREIGN KEY
	(numeroCita)
	REFERENCES Cita
	(numeroCita)
GO

ALTER TABLE Vacuna ADD CONSTRAINT Vacuna_Cita_FK FOREIGN KEY
	(numeroCita)
	REFERENCES Cita
	(numeroCita)
GO

ALTER TABLE PRODUCTO_SANITARIO ADD CONSTRAINT PRODUCTO_SANITARIO_Cita_FK FOREIGN KEY
	(numeroCita)
	REFERENCES Cita
	(numeroCita)
GO

ALTER TABLE Diagnostico ADD CONSTRAINT Diagnostico_Cita_FK FOREIGN KEY
	(numeroCita)
	REFERENCES Cita
	(numeroCita)
GO

ALTER TABLE ADMISIONISTA_HOSPITAL_ORIGEN ADD CONSTRAINT ADMISIONISTA_HOSPITAL_ORIGEN_ESTABLECIMIENTO_SALUD_ORIGEN_FK FOREIGN KEY
	(codigoRenaes)
	REFERENCES ESTABLECIMIENTO_SALUD_ORIGEN
	(codigoRenaes)



GO
Use HcHs
Go


SET DATEFORMAT dmy
Go


/*datos de ESTABLECIMIENT_SALUD */
Insert Into ESTABLECIMIENTO_SALUD VALUES(3742,'Cayetano Heredia','San Martin de Porres')
Insert Into ESTABLECIMIENTO_SALUD VALUES(3741,'Arzobispo Loayza','Lima')
Insert Into ESTABLECIMIENTO_SALUD VALUES(3743,'Santa Rosa','Pueblo Libre')
Insert Into ESTABLECIMIENTO_SALUD VALUES(3744,'Huaycan','Ate')
Insert Into ESTABLECIMIENTO_SALUD VALUES(3745,'Dos de Mayo','Lima')
Insert Into ESTABLECIMIENTO_SALUD VALUES(3746,'Vitarte','Ate')
Insert Into ESTABLECIMIENTO_SALUD VALUES(3747,'Daniel Alcides Carrion','Callao')
GO

/* para ver tablas generales */

SELECT * FROM ESTABLECIMIENTO_SALUD
GO 


/*PPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPP*/
/*datos de ESTABLECIMIENT_SALUD_ORIGEN */
Insert Into ESTABLECIMIENTO_SALUD_ORIGEN VALUES(3741)
Insert Into ESTABLECIMIENTO_SALUD_ORIGEN VALUES(3743)
Insert Into ESTABLECIMIENTO_SALUD_ORIGEN VALUES(3744)
Insert Into ESTABLECIMIENTO_SALUD_ORIGEN VALUES(3745)
Insert Into ESTABLECIMIENTO_SALUD_ORIGEN VALUES(3746)
Insert Into ESTABLECIMIENTO_SALUD_ORIGEN VALUES(3747)
Go

/* para ver tablas generales */
SELECT * FROM ESTABLECIMIENTO_SALUD_ORIGEN
GO 


/*PPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPP*/

/*datos de ESTABLECIMIENT_SALUD_DESTINO  */
Insert Into ESTABLECIMIENTO_SALUD_DESTINO VALUES(3742)
Go
SELECT * FROM ESTABLECIMIENTO_SALUD_DESTINO
GO 

/*PPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPP*/

Insert Into ADMISIONISTA_HOSPITAL_ORIGEN VALUES('Alfredo','Fernandez','ma??ana',3741)
Insert Into ADMISIONISTA_HOSPITAL_ORIGEN VALUES('Rosa','Garcia','ma??ana',3744)
Insert Into ADMISIONISTA_HOSPITAL_ORIGEN VALUES('Fernanda','Cueva','tarde',3743)
Insert Into ADMISIONISTA_HOSPITAL_ORIGEN VALUES('Roberto','Cruz','tarde',3745)
Insert Into ADMISIONISTA_HOSPITAL_ORIGEN VALUES('Tatiana','Sanchez','ma??ana',3746)
Insert Into ADMISIONISTA_HOSPITAL_ORIGEN VALUES('Ana','Vigil','ma??ana',3747)
GO

SELECT * FROM ADMISIONISTA_HOSPITAL_ORIGEN
GO 

/*PPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPP*/
Insert Into ADMISIONISTA_HOSPITAL VALUES('Paty','Campos',3742,'ma??ana')
Insert Into ADMISIONISTA_HOSPITAL VALUES('Maria','Torres',3742,'ma??ana')
Insert Into ADMISIONISTA_HOSPITAL VALUES('Ian','Roca',3742,'tarde')
Insert Into ADMISIONISTA_HOSPITAL VALUES('Manuel','LLanos',3742,'tarde')
Insert Into ADMISIONISTA_HOSPITAL VALUES('Romina','Ramirez',3742,'tarde')
Insert Into ADMISIONISTA_HOSPITAL VALUES('Katherine','Huaman',3742,'ma??ana')
GO

SELECT * FROM ADMISIONISTA_HOSPITAL
GO 

/*PPPPPPPPPPPPPPPPPPPPPPPPPPPP*/





Insert Into Servicio VALUES('Oftalmologia','SI',3742)
Insert Into Servicio VALUES('Neumologia','NO',3742)
Insert Into Servicio VALUES('Cardiologia','SI',3742)
Insert Into Servicio VALUES('Dermatologia','SI',3742)
Insert Into Servicio VALUES('Geriatria','NO',3742)
Insert Into Servicio VALUES('Medicina Interna','SI',3742)
Insert Into Servicio VALUES('Gastroenterologia','SI',3742)
Insert Into Servicio VALUES('Ginecologia','SI',3742)
Insert Into Servicio VALUES('Obstetricia','NO',3742)
Insert Into Servicio VALUES('Urologia','SI',3742)
Insert Into Servicio VALUES('Pediatria','SI',3742)
Insert Into Servicio VALUES('Psicologia','SI',3742)
Insert Into Servicio VALUES('Endocrinologia','SI',3742)
GO

SELECT * FROM Servicio
GO 


/*PPPPPPPPPPPPPPPPPPPPPPPPPPPP*/
Insert Into Departamento VALUES('Medicina')
Insert Into Departamento VALUES('Enfermedades Infecciosas y Dermatologicas')
Insert Into Departamento VALUES('Gineco-Obstetricia')
Insert Into Departamento VALUES('Cirugia')
Insert Into Departamento VALUES('Psicologia')
Insert Into Departamento VALUES('Pediatria')
Go
SELECT * FROM Departamento
Go

/*PPPPPPPPPPPPPPPPPPPPPPPPPPPP*/

Insert Into Especialista VALUES(101,'Carlos', 'Bustamante', 46, '994321910', 'Jiron Retego 123', 'Neumologia', 2001 , 178, 3742)
Insert Into Especialista VALUES(101,'Juan', 'Rivera', 50, '991567194', 'Jiron Tristan 143', 'Cardiologia', 2005 , 111, 3745)
Insert Into Especialista VALUES(101,'Alfonso', 'Atencia', 57, '993573670', 'Calle Alameda 356', 'Neumologia', 1980 , 121, 3112)
Insert Into Especialista VALUES(104,'Carlos', 'Paredes', 47, '992341310', 'Jiron Pleyades 156', 'Oftalmologia', 2005 , 191, 3633)
Insert Into Especialista VALUES(102,'Rossi', 'Ojeda', 38, '997341450', 'Jiron Ursulas 124', 'Dermatologia', 2002 , 141, 3269)
Insert Into Especialista VALUES(101,'Alberto', 'Cedi??o', 38, '957321430', 'Calle Brazil 224', 'Geriatria', 2007 , 191, 3349)
Insert Into Especialista VALUES(101,'Jonathan', 'Ojeda', 58, '955378450', 'Jiron Hifa 191', 'Medicina Interna', 1993 , 122, 4269)
Insert Into Especialista VALUES(101,'Raquel', 'Contreras', 50, '992381496', 'Calle Yellow 121', 'Medicina Interna', 1994 , 132, 4219)
Insert Into Especialista VALUES(101,'Jacobo', 'Diaz', 39, '937642454', 'Jiron Sasdare 177', 'Gastroenterologia', 2009, 143, 4369)
Insert Into Especialista VALUES(101,'Ernesto', 'Perez', 37, '995321476', 'Jiron Pongol 114', 'Gastroenterologia', 2008 , 193, 5159)
Insert Into Especialista VALUES(103,'Rachel', 'Gomez', 49, '93361357', 'Calle Terafo 174', 'Ginecologia', 1991 , 301, 6219)
Insert Into Especialista VALUES(103,'Fredy', 'Sosa', 46, '994371571', 'Calle Tambola 154', 'Obstetricia', 2000 , 352, 7159)
Insert Into Especialista VALUES(104,'Camila', 'Quiroga', 52, '999181459', 'Jiron Max Tello 144', 'Urologia',1990, 356, 7169)
Insert Into Especialista VALUES(104,'Dina', 'Martinez', 38, '924321455', 'Jiron Pierola 126', 'Urologia', 2005 , 442, 5669)
Insert Into Especialista VALUES(106,'Franco', 'Rojas', 49, '923464358', 'Jiron Huaca 174', 'Pediatria', 2000 , 312, 6264)
Insert Into Especialista VALUES(105,'Erika', 'Silva', 51, '994342451', 'Jiron Juli Tello 144', 'Psicologia', 2001 , 362, 5259)
Insert Into Especialista VALUES(101,'Elena', 'Soto', 31, '925351255', 'Jiron Yoshihama 144', 'Endocrinologia', 2005 , 412, 7469)
Insert Into Especialista VALUES(101,'William', 'Morales', 33, '957356780',  'Calle Pleyades 144', 'Endocrinologia', 2001 , 512, 8664)
Go

SELECT * FROM Especialista
Go

Select* From Especialista




/*PPPPPPPPPPPPPPPPPPPPPPPPPPPPP*/

Insert Into Paciente VALUES('Juan','Quispe',35,'M','21/04/1986','juanq15@gmail.com',22594534,134558,'activado','mestizo',122345)
Insert Into Paciente VALUES('Rosa','Perez',25,'F','13/05/1996','rosap@gmail.com',24626748,134559,'suspendido','trigue??a',122346)
Insert Into Paciente VALUES('Damian','Rivera',70,'M','01/04/1951','damirivera@gmail.com',23745345,134560,'activado','mestizo',122347)
Insert Into Paciente VALUES('Roberto','Artigas',18,'M','11/11/2003','roberto.artigas@gmail.com',27463545,134561,'activado','mestizo',122348)
Insert Into Paciente VALUES('Santiago','Ortiz',56,'M','09/11/1965','santiort@gmail.com',27463547,134562,'suspendido','mestizo',122349)
Insert Into Paciente VALUES('Pedro','Orme??o',23	,'M','23/04/1998','pedrito_o@gmail.com',22594534,134563,'activado','trige??a',122350)
Insert Into Paciente VALUES('Liz','Duran',16,'F','30/5/2005','liz.duran@gmail.com',76534224,134564,'suspendido','mestizo',122351)
Insert Into Paciente VALUES('Jabes','Montoya',17,'M','25/12/2004','jabemon5@gmail.com',76354453,134565,'activado','moreno',122352)
Insert Into Paciente VALUES('Nicole','Jaramillo',31,'F','03/09/1990','nicoj.10@gmail.com',23857455,134566,'suspendido','mestizo',122353)
Insert Into Paciente VALUES('Mabel','Bazan',6,'F','14/06/2015','mabeb@gmail.com',74527384,134567,'activado','morena',122354)

/* adolescentes 12-18  */
Insert Into Paciente VALUES('Julio','Orme??o',12,'M','05/12/2009','juanq15@gmail.com',72894534,134558,'activo','mestizo',122345)
Insert Into Paciente VALUES('Karen','Hinostroza',17,'F','05/12/2004','karen158@gmail.com',72784534,454858,'cancelado','moreno',122335)
Insert Into Paciente VALUES('Katia','Arevalo',16,'F','05/11/2005','katia163@gmail.com',72304834,410468,'activo','mestizo',124675)
Insert Into Paciente VALUES('Renato','Diaz',17,'M','06/08/2004','renato13@gmail.com',70374734,402468,'cancelado','mestizo',104175)
Insert Into Paciente VALUES('Flor','Lalupu',16,'F','05/09/2005','flor63@gmail.com',70304874,412461,'activo','mestizo',157625)
Insert Into Paciente VALUES('Estrella','Nu??ez',17,'F','06/07/2004','ter@gmail.com',73304804,417018,'suspendido','mestizo',101665)
Insert Into Paciente VALUES('Miguel','Labrin',18,'M','06/10/2003','mig63@gmail.com',77153814,412018,'activo','mestizo',606625)
Insert Into Paciente VALUES('Rosalia','Nu??ez',17,'F','06/09/2004','rod63@gmail.com',76354534,342408,'suspendido','mestizo',134005)
Insert Into Paciente VALUES('Luis','Quispe',17,'M','06/10/2004','luiq63@gmail.com',71006894,712058,'activo','mestizo',104571)

/*Jovenes 19-29 */
Insert Into Paciente VALUES('Abel','Paniahua',21,'M','02/04/2000','abp632@gmail.com',71808814,704038,'suspendido','moreno',124371)
Insert Into Paciente VALUES('Karina','Lapeciere',24,'F','04/06/1997','karlap894@gmail.com',74208564,746788,'activo','moreno',157091)
Insert Into Paciente VALUES('Valentino','Guadamur',23,'M','06/08/1998','valenguad67@gmail.com',73855864,714068,'activo','mestizo',190351)
Insert Into Paciente VALUES('Cesar','Pariachi',26,'M','07/03/1995','cesarpar45@gmail.com',71808814,704038,'suspendido','mestizo',136071)
Insert Into Paciente VALUES('Augusto','Lipian',26,'M','05/01/1995','asretg45@gmail.com',70345864,732567,'activo','moreno',336571)
Insert Into Paciente VALUES('Amanda','Matto',25,'F','04/03/1996','amanmtpp@gmail.com',74358854,754678,'activo','mestizo',146567)
Insert Into Paciente VALUES('Brenda','Acevedo',23,'F','07/03/1995','cesarpar45@gmail.com',71808814,704038,'suspendido','mestizo',136071)
Insert Into Paciente VALUES('Fabio','Kara',22,'M','04/04/1999','FABKA13@gmail.com',71855874,764631,'activo','moreno',135561)
Insert Into Paciente VALUES('Angello','Mandez',21,'F','06/09/2000','ang125@gmail.com',71405617,745618,'activo','mestizo',133411)


/* ni??os 0  a 9 a??os */
Insert Into Paciente VALUES('Liam', 'Lopez', 4, 'M', '16/06/2017', '-', 16468465,276887, 'activo', 'mestizo', 134486)
Insert Into Paciente VALUES('Olivia', 'Vargas', 6, 'F', '28/04/2015', '-', 35484637,464684, 'suspendido', 'trige??o', 165798)
Insert Into Paciente VALUES('Albert', 'Toledo', 7, 'M', '09/11/2014', '-', 87354354,654635, 'activo', 'moreno', 176358)
Insert Into Paciente VALUES('Roberto', 'Ramirez', 2, 'M', '18/03/2019', '-', 76411324,354354, 'activo', 'moreno', 168335)
Insert Into Paciente VALUES('Emma', 'Mendoza', 1, 'F', '30/11/2020', '-', 38965666,786315, 'activo', 'trige??o', 186645)
Insert Into Paciente VALUES('Eva', 'Chamo', 9, 'F', '12/12/2012', '-', 87264654,534379, 'suspendido', 'mestizo', 135548)
Insert Into Paciente VALUES('Ada', 'Cumba', 1, 'F', '31/08/2020', '-', 31643454,647869, 'activo', 'mulato', 134433)
Insert Into Paciente VALUES('Charlotte', 'Gomez', 6, 'F', '24/04/2015', '-', 45313435,341343, 'suspendido', 'moreno', 146335)
Insert Into Paciente VALUES('Victoria', 'Robles', 5, 'F', '21/02/2016', '-', 43143415,354115, 'suspendido', 'mestizo', 187636)
Insert Into Paciente VALUES('Mia', 'Zarate', 3, 'F', '16/07/2018', '-', 71799792,684335, 'activo', 'trige??o', 199866)

/*Jovenes 29-50 eeeeee */
Insert Into Paciente VALUES('Sebastian', 'Montes', 44, 'M', '06/09/1977', 'sebastianmontes@gmail.com', 45456428,151512, 'suspendido', 'moreno', 124865)
Insert Into Paciente VALUES('Harry', 'Potter', 36, 'M', '05/12/1985', 'harrypotter@gmail.com', 82651595,151685, 'activo', 'mestizo', 145256)
Insert Into Paciente VALUES('Mariana', 'Suarez', 48, 'F', '24/06/1973', 'mariana21suarez@gmail.com', 46621689,146198, 'activo', 'trige??a', 128465)
Insert Into Paciente VALUES('Mark', 'Evans', 39, 'M', '15/02/1982', 'marevans23@gmail.com', 16543515,561468, 'suspendido', 'moreno', 148626)

Insert Into Paciente VALUES('Celia', 'Torca', 24, 'F', '04/12/1997', 'celiator12@gmail.com', 14642879,164645, 'activo', 'moreno', 176168)

Insert Into Paciente VALUES('Rimuru', 'Tempest', 27, 'M', '15/06/1994', 'rimurtemp54@gmail.com', 14648633,165155, 'activo', 'trige??a', 166755)
Insert Into Paciente VALUES('Fitz', 'Samas',67, 'M', '08/11/1954', 'fitzsam13@gmail.com', 46842349,464628, 'suspendido', 'mestizo', 164869)
Insert Into Paciente VALUES('Dango', 'Gutierrez', 47, 'M', '01/11/1974', 'dangoguti@gmail.com', 76448649,768685, 'activo', 'moreno', 179925)
Insert Into Paciente VALUES('Kevin', 'Albino', 49, 'M', '19/08/1972', 'kevialbin@gmail.com', 65866527,464556, 'suspendido', 'trige??o', 168438)
Insert Into Paciente VALUES('Steve', 'Cacho', 36, 'M', '28/09/1985', 'steve-cacho12@gmail.com', 16682648,684665, 'activo', 'mestizo', 152662)

/*Adultos mayores 50-++ */
Insert Into Paciente VALUES('Paolo','Farfan',71,'M','10/06/1950','-',23485485,39453,'activo','mestizo',485834)
Insert Into Paciente VALUES('Jose','Estrada',69,'M','04/11/1952','-',24583473,32394,'suspendido','mestizo',319453)
Insert Into Paciente VALUES('Emilia','Drago',60,'F','06/10/1961','-',24583845,49295,'activo','mestizo',756312)
Insert Into Paciente VALUES('Raul','Bocanegra',72,'M','04/10/1949','-',24583753,966345,'suspendido','moreno',984623)
Insert Into Paciente VALUES('Salvador','Gonzales',66,'M','06/10/1955','-',24858457,35925,'activo','mestizo',313854)
Insert Into Paciente VALUES('Sonia','Belaunde',65,'F','06/10/1956','-',24857345,55531,'suspendido','trigue??a',313845)
Insert Into Paciente VALUES('Miguel','Sanchez',68,'M','05/10/1953','-',24948573,44528,'activo','mestizo',133551)
Insert Into Paciente VALUES('Sergio','Huaman',65,'M','04/12/1956','-',78483920,11045,'activo','mestizo',444633)
GO


SELECT * FROM Paciente
Go


/*PPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPPP*/
Insert Into Cita VALUES('Cardiologia','10:15','05/12/2021',NULL,'Cita',10144,1256,1477,5832147)
Insert Into Cita VALUES('Medicina Interna','16:00','15/03/2021',NULL,'Cita',10150,1258,1478,5832148)
Insert Into Cita VALUES('Pediatria','16:30','24/01/2021',NULL,'Cita',10157,1259,1479,5832174)
Insert Into Cita VALUES('Medicina Interna','11:30','02/12/2021',NULL,'Cita',10150,1258,1476,5832146)
Insert Into Cita VALUES('Cardiologia','12:30','05/03/2021','10/04/21','Emergencia',10144,1260,1480,5832178)
Insert Into Cita VALUES('Psicologia','13:30','23/04/2021',NULL,'Cita',10158,1256,1478,5832184)
Insert Into Cita VALUES('Neumologia','15:00','12/01/2021',NULL,'Cita',10143,1258,1478,5832162)
Insert Into Cita VALUES('Obstetricia','16:42','24/08/2021','28/08/2021','Emergencia',10154,1257,1478,5832169)
Insert Into Cita VALUES('Oftalmonogia','15:00','05/03/2021','05/03/2021','Cita',10146,1260,1478,5832170)
Insert Into Cita VALUES('Pediatria','10:30','24/11/2021',NULL,'Cita',10157,1257,1476,5832182)
Insert Into Cita VALUES('Medicina Interna','11:30','02/10/2021',NULL,'Cita',10150,1256,1477,5832183)
Insert Into Cita VALUES('Cardiologia','15:30','06/09/2021','16/09/21','Emergencia',10144,1257,1478,5832189)
INSERT INTO Cita VALUES('Endocrinologia','13:45','22/04/2021','26/04/2021','Emergencia',10159,1256,1478,5832185)
INSERT INTO Cita VALUES('Dermatologia','18:00','27/05/2021','27/05/2021','Cita',10147,1259,1479,5832171)
INSERT INTO Cita VALUES('Gastroenterologia','10:00','01/04/2021','03/04/2021','Emergencia',10151,1260,1476,5832172)
Go

SELECT * FROM Cita
Go

DELETE FROM Cita



Insert into PRODUCTO_FARMACEUTICO VALUES ('Amoxicilina','250mg/5mlLX 60 mL','SUS',3744)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Mebendazol', '200mg+40 mg/5mL x 60 mL', 'SUS',3756)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Oxitocina', '100mg/5mLx 30 mL', 'SUS',3749)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Paracetamol', '10 UI', 'INY',3743)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Sulfato Ferroso', '120 mg/5 mL x 60 mL','JBE',3742)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Multimicronutrientes', '400ug+60mg Fe', 'TAB',3751)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Acido Folico', '12.5 mg Fe', 'SB1',3754)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Albiglutida', '15mg Fe/5mL x 180 mL', 'JBE',3745)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Sulfametoxazol', '14.5mg/ 4mLx 25mL', 'TA2',3746)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Alogliptina', '125mg/4mLx 15mL', 'CFF',3748)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Amobarbital', '500MG/3mLX 12 mL', 'SUS',3747)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Azitromicina', '14 UI', 'JBE',3750)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Apalutamide', '12mg/ 4mLx 13mL', 'TAB',3752)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Arginine','12UI','SUS',3755)
Insert into PRODUCTO_FARMACEUTICO VALUES ('Crizotinib', '250mg/ 5mLx 15mL', 'INY',3753)
GO


/*PPPPPPPPPPPPPPPPPPPPPPPPPPPPP*/
Insert into PRODUCTO_SANITARIO VALUES ('CEPILLO DENTAL','Fsa','18g',3744)
Insert into PRODUCTO_SANITARIO VALUES ('PASTAS DENTRIFICAS','Tbo','90g',3744)
Insert into PRODUCTO_SANITARIO VALUES ('Desfibrilador', 'Gvt','5.15kg',3746)
Insert into PRODUCTO_SANITARIO VALUES ('Aud??fono', 'Fes', '268g',3751)
Insert into PRODUCTO_SANITARIO VALUES ('Bajalenguas', 'Dav', '0.28g',3752)
Insert into PRODUCTO_SANITARIO VALUES ('Implante dental', 'Sus', '11g',3751)
Insert into PRODUCTO_SANITARIO VALUES ('Estetoscopio', 'Sus', '20kg',3752)
Insert into PRODUCTO_SANITARIO VALUES ('Equipo RX', 'Hyt', '3.8kg',3756)
Insert into PRODUCTO_SANITARIO VALUES ('Bolsas de orina', 'Gks', '17g',3742)
Insert into PRODUCTO_SANITARIO VALUES ('Vendas', 'Hts', '74g',3755)
Insert into PRODUCTO_SANITARIO VALUES ('Guantes', 'Tab', '4.5g',3755)
Insert into PRODUCTO_SANITARIO VALUES ('Jeringuillas', 'Sbs', '1g',3754)
Insert into PRODUCTO_SANITARIO VALUES ('Agujas', 'Fat', '115g',3747)
Insert into PRODUCTO_SANITARIO VALUES ('M??quinas de anestesia', 'Ags', '15kg',3753)
Insert into PRODUCTO_SANITARIO VALUES ('Term??metros', 'Ftg', '270g',3748)
GO

/*PPPPPPPPPPPPPPPPPPPPPPPPPPPPP*/
Insert into Vacuna VALUES ('Influenza', '1',3742)
Insert into Vacuna VALUES ('Parotid', '2',3743)
Insert into Vacuna VALUES ('Rubeola', '2',3744)
Insert into Vacuna VALUES ('RotaVirus', '1',3745)
Insert into Vacuna VALUES ('Antiamarilica', '3',3746)
Insert into Vacuna VALUES ('Antineumoc', '1',3747)
Insert into Vacuna VALUES ('Antitetanica', '1',3748)
Insert into Vacuna VALUES ('VPH', '2',3749)
Insert into Vacuna VALUES ('IPV', '2',3750)
Insert into Vacuna VALUES ('Pentaval', '1',3751)
GO

