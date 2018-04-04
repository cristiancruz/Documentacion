# SAILS
------------

- **CONFIGURACIÓN EQUIPO**

------------
1.  Ejecutar :  **npm install sails -g**
1.  Ejecutar :  **sails new name_project**
2. Generar proyecto:
	- Ejecutar **sails new name_project**
	- Seleccionar la opcion 1(TEMPLATE) o para 2 (API)
1.  Levantar server:
	- **sails lift**
	- Acceder desde : http://localhost:1337/
------------

**CONFIGURACIÓN API**

------------
1.  En config/datastores descomentar y cambiar valores:
	 1. **adapter: 'sails-mysql'**
	1. **url:'mysql://user:password@host:port/database'**
1. En config/blueprints descomentar:
	 1. **rest: true**
	1. **shortcuts: false**
1. En config/security descomentar:
	 1. **allRoutes: true**
	1. origin:'*' // Cambiar a url del cliente(react,angular).
1.  En config/i18n cambiar:
	 1. **defaultLocale: 'es'**
1.  En config/models descomentar:
	 1. **migrate: 'alter'** // revisar en produccion cual revisar.
------------

**CLI, MODELOS, CONTROLADORES, RUTAS**

------------

1. Generar api (model, controller):
	- Ejecutar **sails generate api name** 
	//Esto generara un modelo Name y un controlador NameController con rutas automaticas REST
	- Rutas generadas automaticamente:
    	 1. **name  => GET**
    	 1. **name/:id    	=> GET**
    	 1. **name   	=> POST**
    	 1. **name/:id    	=> PATCH**
    	 1. **name/:id   	=> DELETE**
	- Metodos en controlador:
	 1. Dirigirse a api/controllers/NameController, estara vacio pero implicitamente las rutan anteriores trabajan con los metodos siguientes, en caso de  querer obtener mas informacion en alguna ruta esta tiene que ser sobreescrita en el controlador como en las rutas (config/routes) ejemplo('GET /url': 'NameController.method'):
	 
		 - **name  => GET** =  index
		 -  **name/:id    	=> GET** = pendiente
		 -  **name   	=> POST** = create
		 -  **name/:id    	=> PATCH** = update
		 -  **name/:id   	=> DELETE** =  destroy
1. Trabajar con los modelos:
	- Dirigirse a api/model/nameModel y ahi agregar los campos requeridos, un ejemplo seria:
			module.exports = {
 			 attributes: {
				name:{
			        type: 'string',
					  defaultsTo:'Cristian'
					},
					last_name:{
					  type:'string',
					  required:true
					},
					email:{
					  type:'string',
					  required:true,
					  unique: true
					},
					profile: {
						type: 'string',
						enum: ['normal', 'admin'],
						defaultsTo: 'normal'
					},
					year: {
						type: 'integer',
						required:true
					},
					active: {
						type: 'boolean',
						defaultsTo: true
						},
						avatarUrl: {
							type: 'string'
					},
					profile: {
						collection: 'profile',
						via: 'user'
					}
				},
			};