--<ScriptOptions statementTerminator="GO"/>

CREATE TABLE Servicio (
		nombre VARCHAR(20) NOT NULL,
		disponibilidad CHAR(2) NOT NULL,
		codigoUPS INTEGER NOT NULL,
		codigoPrestacion INTEGER NOT NULL IDENTITY (1,1),
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
		corteTardioCordon CHAR(1) NOT NULL,
		edadGestacional INTEGER NOT NULL,
		PACIENTE_ID INTEGER NOT NULL
	)
GO

CREATE TABLE PACIENTE_FEMENINO (
		fechaProbableParto DATETIME NULL,
		saludMaterna CHAR(10) NULL,
		alturaUterina INTEGER NULL,
		edadGestacional INTEGER NULL,
		partoVertical CHAR(2) NULL,
		PACIENTE_ID INTEGER NOT NULL
	)
GO

CREATE TABLE Adolescente (
		perimetroAbdominal VARCHAR(10) NULL,
		IMC VARCHAR(10) NULL,
		PACIENTE_ID INTEGER NOT NULL
	)
GO

CREATE TABLE Paciente (
		nombres VARCHAR(20) NOT NULL,
		apellidos VARCHAR(20) NOT NULL,
		edad INTEGER NOT NULL,
		sexo CHAR(1) NOT NULL,
		fechaNacimiento DATETIME NOT NULL,
		correoElectronico VARCHAR(30) NOT NULL,
		dni INTEGER NOT NULL,
		codigoSIS INTEGER NOT NULL,
		estadoSeguro VARCHAR(10) NOT NULL,
		numeroHistoriaClinica INTEGER NOT NULL,
		etnia VARCHAR(15) NOT NULL,
		PACIENTE_ID INTEGER NOT NULL IDENTITY (1,1)
	)
GO

CREATE TABLE ADMISIONISTA_HOSPITAL (
		codAdmiD INTEGER NOT NULL IDENTITY (1,1),
		nombres VARCHAR(20) NULL,
		codigoRenaes INTEGER NOT NULL
	)
GO

CREATE TABLE Cita (
		lugarAtencion VARCHAR(18) NOT NULL,
		atencion VARCHAR(18) NOT NULL,
		hora VARCHAR(10) NOT NULL,
		nombreServicio VARCHAR(10) NOT NULL,
		fechaIngreso DATETIME NOT NULL,
		fechaAlta DATETIME NULL,
		destinoAsegurado VARCHAR(10) NOT NULL,
		numeroCita INTEGER NOT NULL IDENTITY (1,1),
		codigoEspecialista INTEGER NOT NULL,
		codAdmior INTEGER NOT NULL,
		codAdmiD INTEGER NOT NULL,
		PACIENTE_ID INTEGER NOT NULL
	)
GO

CREATE TABLE Especialista (
		nombres CHAR(20) NOT NULL,
		apellidos CHAR(20) NOT NULL,
		edad INTEGER NOT NULL,
		numeroCelular INTEGER NOT NULL,
		direccion VARCHAR(30) NOT NULL,
		especialidad VARCHAR(20) NOT NULL,
		añoContrato VARCHAR(4) NOT NULL,
		numeroColegiatura INTEGER NOT NULL,
		numeroRNE INTEGER NOT NULL,
		numeroEspecialista INTEGER NOT NULL,
		codigoEspecialista INTEGER NOT NULL IDENTITY (1,1),
		DEPARTAMENTODEPARTAMENTO_ID INTEGER NOT NULL
	)
GO

CREATE TABLE Departamento (
		nombreDepartamento CHAR(10) NOT NULL,
		DEPARTAMENTO_ID INTEGER NOT NULL IDENTITY (1,1)
	)
GO

CREATE TABLE PRODUCTO_FARMACEUTICO (
		nombre VARCHAR(18) NOT NULL,
		concentracion VARCHAR(10) NOT NULL,
		formaFarmaceutica VARCHAR(10) NOT NULL,
		codigoMedicamento INTEGER NOT NULL IDENTITY (1,1),
		numeroCita INTEGER NOT NULL
	)
GO

CREATE TABLE Vacuna (
		nombreVacuna VARCHAR(10) NOT NULL,
		numeroDosis INTEGER NOT NULL,
		codigoVacuna INTEGER NOT NULL IDENTITY (1,1),
		numeroCita INTEGER NOT NULL
	)
GO

CREATE TABLE PRODUCTO_SANITARIO (
		nombre CHAR(10) NULL,
		presentacion CHAR(10) NULL,
		caracteristica CHAR(10) NULL,
		codigoProductoSan INTEGER NOT NULL IDENTITY (1,1),
		numeroCita INTEGER NOT NULL
	)
GO

CREATE TABLE Diagnostico (
		afeccion VARCHAR(15) NOT NULL,
		tipoDiagnostico VARCHAR(10) NOT NULL,
		codigoDiagnostico INTEGER NOT NULL IDENTITY (1,1),
		numeroCita INTEGER NOT NULL
	)
GO

CREATE TABLE ADMISIONISTA_HOSPITAL_ORIGEN (
		nombres VARCHAR(20) NOT NULL,
		codAdmior INTEGER NOT NULL IDENTITY (1,1),
		codigoRenaes INTEGER NOT NULL,
		turnoTrabajo VARCHAR(10) NOT NULL
	)
GO

CREATE TABLE ESTABLECIMIENTO_SALUD (
		codigoRenaes INTEGER NOT NULL,
		distrito VARCHAR(20) NOT NULL,
		nombreEstablecimiento VARCHAR(20) NOT NULL
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

