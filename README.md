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
   Descargar las llaves ssh privada y pública, luego Next, Next y Create

	<<img width="2169" height="920" alt="image" src="https://github.com/user-attachments/assets/0f4f1152-a20c-4efa-8fa4-2860a2cbdb5a" />

	<img width="1309" height="453" alt="image" src="https://github.com/user-attachments/assets/0eb73fa0-e638-48b8-b520-25dd0ca7ae21" />

3. Crear Load Balancer
	Menú -> Networking -> Load balancer -> Create load balancer
	<img width="1579" height="683" alt="image" src="https://github.com/user-attachments/assets/5159c7be-d0fe-46ba-97e8-0d6fc9e4855c" />

	Selecionar
	```
	CAMPO				VALOR
	==============================================
 	VCN:	 			VCN_NOMBRE_stgo
	Subnet				public subnet-VCN_NOMBRE_stgo
 	```
	<img width="2163" height="617" alt="image" src="https://github.com/user-attachments/assets/47242896-ca6c-4dcd-a1ce-1cc72bf0657e" />

	Selecionar la instancia creada como backend

	<img width="2175" height="997" alt="image" src="https://github.com/user-attachments/assets/f702ee33-be37-4529-b3f6-07579b420c7a" />

	Cambiar el protocolo a HTTP y dar click en next
	<img width="1354" height="617" alt="image" src="https://github.com/user-attachments/assets/66efd143-cbcc-4b51-9aea-1c7dfde271e4" />

	Deshabilitar los logs de error y click en next

	<img width="1344" height="736" alt="image" src="https://github.com/user-attachments/assets/ef87d16f-351f-46d4-a75b-87dfaeec7111" />

	Revisar los detalles finales y click en Submit

	<img width="2184" height="928" alt="image" src="https://github.com/user-attachments/assets/33645d98-5536-4a20-8151-821396a46694" />

5. Crear el bucket que se utilizará para el proceso de migración
	Menú -> Storage -> Bucket

	<img width="1683" height="576" alt="image" src="https://github.com/user-attachments/assets/cebecf45-fc48-463b-aaf6-77b85768bd8c" />

	Repetir la misma creación en Valparaíso, pero sin asignar backend

7. Al finalizar la creación del LB, configurar FSDR

	Menú -> Migration & Recovery -> Disaster Recovery

	<img width="1722" height="649" alt="image" src="https://github.com/user-attachments/assets/8cb77505-f0d4-43b3-929e-e18c43810fb7" />

	Selecionar
	```
	CAMPO				VALOR
	==============================================
 	Bucket Name:	 	bucket_NOMBRE_FSDR_stgo
	Bucket Scope:		Namespace
 	```
 	Luego click en Create bucket

	<img width="2170" height="935" alt="image" src="https://github.com/user-attachments/assets/bc17b3ec-5fd1-435d-83d8-0a471ef3d6d0" />

	Este precedimiento se debe realizar también en la región de Valparaíso
	
	Selecionar
	```
	CAMPO				VALOR
	==============================================
 	Bucket Name:	 	bucket_NOMBRE_FSDR_valpo
	Bucket Scope:		Namespace
 	```
 	Luego click en Create bucket

9. Crear Protection Group
	Menú -> Migration & Recovery -> Disaster Recovery

	<img width="1781" height="665" alt="image" src="https://github.com/user-attachments/assets/8e3b4b6d-d151-4228-bb19-04e46e881023" />

	Selecionar
	```
	CAMPO				VALOR
	==============================================
 	Name:			 	DRG_NOMBRE_stgo
	Bucket:				bucket_NOMBRE_FSDR_stgo
 	Role:				Not configured
 	```
 	Luego click en Create	

	<img width="2170" height="928" alt="image" src="https://github.com/user-attachments/assets/3fed689f-3785-4bdb-824c-9bd5753a1c97" />

	Este mismo proceso se debe realizar en la región de Valparaíso

	Selecionar
	```
	CAMPO				VALOR
	==============================================
 	Name:			 	DRG_NOMBRE_valpo
	Bucket:				bucket_NOMBRE_FSDR_stgo
 	Role:				Not configured
 	```
 	Luego click en Create	

10. Una vez creados los DR group, se debe configurar el peer entre ellos

	Entrar al DRG -> Action -> Associate
	<img width="1915" height="671" alt="image" src="https://github.com/user-attachments/assets/4f977956-0a8c-4a4f-b280-9047e40d04f7" />

	En el DRG de Santiago definir:
	```
	CAMPO				VALOR
	==============================================
 	Role:			 	Primary
	Peer Region:		Chile West (Valparaiso)
 	Peer compartment:	FSDR_valpo
 	Peer DR Group:		DRG_valpo
 	```
 	Click en Associate
 
	<img width="1" height="1" alt="image" src="https://github.com/user-attachments/assets/38b71268-3870-4892-a3a2-437bf9c508d9" />

12. Dentro del DRG de Santiago, hacer click en la pestaña Members y Manage members

	<img width="1913" height="727" alt="image" src="https://github.com/user-attachments/assets/98881d19-4fef-4e52-a9c2-58b5ef420d1c" />

	Hacer click en Add member y selecionar Compute -> Instance dentro de Resource type 

	<img width="2188" height="998" alt="image" src="https://github.com/user-attachments/assets/70e747d7-3756-468b-a53f-882f4f6e9333" />

	Buscar la instancia creada y agregarla
	
	<img width="1290" height="596" alt="image" src="https://github.com/user-attachments/assets/397661d1-abc5-4a70-b627-c935191d31ad" />

	Luego hacer click en Add VNIC mapping

	<img width="1295" height="413" alt="image" src="https://github.com/user-attachments/assets/79c57917-b79e-4e15-a562-d433320f6535" />

	Selecionar la vnic y subnets que correspondan
	```
	CAMPO				VALOR
	==============================================
 	VNIC:			 	vnic_instancia_stgo
	Dest. Compartment:	FSDR_valpo
 	Destination VCN:	VCN_valpo
 	Dest. compartment: 	private subnet-VCN_valpo (regional)
 	Dest IP: 			La ip de la instancia creada
 	```
 	Click en Add

	<img width="1740" height="931" alt="image" src="https://github.com/user-attachments/assets/c8f273eb-5781-431e-ae11-d0a7972d5978" />

	Finalmente click en Add

	<img width="1724" height="929" alt="image" src="https://github.com/user-attachments/assets/5d965597-fa6a-4593-92e0-fc356d35acb0" />


14. Una vez finalizado el proceso de agragar la instancia, se debe agregar el LB

	Hacer click en Add member y selecionar Networking -> Load Balancer

	<img width="1739" height="940" alt="image" src="https://github.com/user-attachments/assets/208a321b-3026-49e2-899d-b1fce9a84710" />

	Mapear el LB y el backendset de Santiago con los de Valparaíso. Importante validar los compartmente que correspondan, luiego click en Add 

	<<img width="1720" height="827" alt="image" src="https://github.com/user-attachments/assets/6078d916-40cb-4739-960b-c296972cf6f4" />

	


16. 
17. adsads
18. ads
19. a
20. ds
21. ads
22. ads
23. dsa
24. ads
25. ds
26. a
27. ads
28. das
29. dsa
30. ads
31. dsa
32. 


