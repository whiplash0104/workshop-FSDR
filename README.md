### Requerimientos:
- Cuenta de Oracle Cloud Infrastructure(test gratuito https://www.oracle.com/cloud/free/)
- Cuenta de Github (https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home)



### Paso a Paso
0. Crear Compartment FSDR en Stgo y Valparaíso
	Santiago
	Menu -> Identity & Security -> Compartmente -> New Compartment
	```
	CAMPO				VALOR
	==============================================
	Name		 		        FSDR_NOMBRE_stgo     
	Description 			  FSDR_NOMBRE
	Parent Compartment 	XXXX (root)
	```
 
	Valparaíso
 	Menu -> Identity & Security -> Compartmente -> New Compartment
	```
	CAMPO				VALOR
	==============================================
	Name		 		        FSDR_NOMBRE_valpo    
	Description 			  FSDR_NOMBRE
	Parent Compartment 	XXXX (root)
	```
 	<img width="1343" height="587" alt="image" src="https://github.com/user-attachments/assets/f5b6c907-7ffa-40db-8187-18602aaaba7c" />

	<img width="2157" height="917" alt="image" src="https://github.com/user-attachments/assets/316d2868-9247-4d0c-9a81-b35e6a89919a" />

	
 	<img width="1918" height="499" alt="image" src="https://github.com/user-attachments/assets/e10466bf-41fc-41c0-8a61-5e8102b7f09b" />

	Para cambiar de región se debe selecionar se deben desplegar desde el apartado de regiones

	<img width="809" height="337" alt="image" src="https://github.com/user-attachments/assets/1783c98e-48fb-43fd-9ee9-c947f096b154" />


1. Crear VCN en cada región, en ambas VCN dejar los mismos rangos de IP que vienen por default
	Santiago:
	Menú -> Networking -> VNC -> Action -> Start VCN Wizard -> Create VCN with Internet Connectivity -> Start VCN Wizard
	```
	CAMPO				VALOR
	==============================================
 	Name:	 			VCN_NOMRE_stgo
 	Compartment:		FSDR_NOMRE_stgo
 	```

 	Valparaíso:
	Menú -> Networking -> VNC -> Action -> Start VCN Wizard -> Create VCN with Internet Connectivity -> Start VCN Wizard
	```
	CAMPO				VALOR
	==============================================
 	Name:	 			VCN_NOMRE_valpo
 	Compartment:		FSDR_NOMRE_valpo
 	```
	<img width="1542" height="828" alt="image" src="https://github.com/user-attachments/assets/26c96506-7cf7-4f49-9c02-287975833775" />

	<img width="1215" height="555" alt="image" src="https://github.com/user-attachments/assets/0f8fc60a-a757-49e4-b113-a4fff124302c" />

	<img width="1736" height="920" alt="image" src="https://github.com/user-attachments/assets/02de7989-3446-454f-9e9d-add76be68f5c" />

	<img width="965" height="693" alt="image" src="https://github.com/user-attachments/assets/44da6f27-5b70-4d6c-b4d5-2dd8e22f0bf7" />



2. Una vez creadas las VCN en la región de *Santiago*, crear una VM dentro del compartment FDSR_NOMBRE_stgo
	Compute -> Instances -> Create Instance
	<img width="1195" height="758" alt="image" src="https://github.com/user-attachments/assets/55e0d8b5-d332-49df-8902-d05e4d9d8947" />
	
	```
	CAMPO				VALOR
	==============================================
 	Name:	 			instancia_NOMBRE_stgo
 	Compartment:		FSDR_NOMRE_stgo
 	Shape: 				AMD, VM.Standard.E5.Flex
 	```
   Dejar todo el resto sin cambios y Next

	<img width="2178" height="955" alt="image" src="https://github.com/user-attachments/assets/87ca8107-762a-4c91-833e-6f09e15db112" />

	<img width="1724" height="924" alt="image" src="https://github.com/user-attachments/assets/49630827-8df4-47d2-afab-9e8892db3644" />


	```
	CAMPO				VALOR
	==============================================
 	VNIC:	 			vnic_instancia_NOMBRE_stgo
	Subnet				private subnet-VCN_NOMBRE_stgo
 	```
   Validar que el compartment sea FSDR_NOMRE_stgo, que la VCN sea VCN_NOMBRE_stgo y la subnet
   Descargar las llaves ssh privada y opública, luego Next, Next y Create

	<<img width="2169" height="920" alt="image" src="https://github.com/user-attachments/assets/0f4f1152-a20c-4efa-8fa4-2860a2cbdb5a" />

	<img width="1309" height="453" alt="image" src="https://github.com/user-attachments/assets/0eb73fa0-e638-48b8-b520-25dd0ca7ae21" />

4. das
5. das
6. adsads
7. ads
8. a
9. ds
10. ads
11. ads
12. dsa
13. ads
14. ds
15. a
16. ads
17. das
18. dsa
19. ads
20. dsa
21. 


