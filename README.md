# Evidencia_1F
Evidencia Reporte

• Uso del programa.

• Créditos.
 
• Licencia.

La documentación de la aplicación se debe manejar en GitHub en el área de Wiki y las secciones con las que debe contar son: 
• Acerca de: se explica brevemente la aplicación.
La aplicación cuenta con un usuario inicial y contraseña, el cual depende de los datos ingresados es la elección de del siguiente menú que inicia como administrador o hace referencia de que es paciente.
El menú de administrador cuenta con las siguientes características:
Alta de doctor, requiere el nombre completo del doctor y su especialidad de igual manera se genera un Id.
Alta de paciente, requiere nombre de paciente y de igual manera se genera un Id.
Agendar cita con fecha y hora, se genera un Id, requiere que se coloque una fecha y hora, motivo por el cual se agenda la cita, Id del doctor y el Id paciente, es necesario ingresar todos los datos para que no se guarde en blanco.
Mostrar lista de citas, se genera un listado de las citas ingresadas mostrando por fechas.
Salir, agradece por la visita.
La aplicación 
• Proyecto: incluir el diagrama de flujo en la entrega uno, además de describir cada una de las clases incluidas, su propósito y descripción de sus métodos y variables. 
 
ClasePrincipal.
Cuenta con amplia librería las variables a utilizar db la cual se utiliza en su método de crear carpeta inexistente, pacientes se utiliza en el método carga de paciente, para dar de alta, variable Doctor, se utiliza en el método Carga de Doctor para dar de alta al doctor y su especialidad.
La variable cita, se utiliza en el método cargar cita esto es para ingresar los datos requeridos como fecha, hora IdPaciente, IdDoctor y motivo.
La variable Admin usuario es la que se va a validar junto con el pasword para permitir el ingreso al medu el cual esta categorizado con las demás clases.
El método ejecutar es el que da la bienvenida al usuario y va a requerir de sus credenciales como usuario y contraseña, en caso de ser correctos va a permitir el acceso al siguiente menú en caso contrario va a enviar un mensaje de usuario o contraseña incorrecto, intente nuevamente.
El método autenticacionAdministracdores donde permite ingresar las credenciales usuario y contraseña.
Método cargaDatos como su nombre lo indica es el encargado de cargar los datos Doctor, Paciente y cita.
Método cargaDorctor realizado con un try, cash con una variable de br por las siglas BuffersdReader el cual permite cargar los datos del doctor Id, Nombre y especialidad, en caso de generar un error al momento de carga de datos enviara un mensaje el cual ara mención del error y mostrara el tipo de error por e.getmessage.
Método cargaPaciente es similar al de carga de doctores solo en esta carga el Id y el nombre,
Método carga de citas solo que en este se va a cargar la fecha, hora, Id doctor y id Paciente, los tre métodos se manejan de sibilancia igual, por ser método de cargado de datos.
El método altaDoctor genera un Id nuevo pidiendo nombre completo y especialidad, de igual manera es la cargaPaciente solo con la diferencia solo requiere el nombre ya que se genera un _Id nuevo.
Método generarNeuvoIdPaciente, generarNeuvoIdPaciente es el generador de Id por automático ya que cuenta con un incrementado, ambos sirven de igual manera.
Método crearCita es el que permite ingresar los datos mencionados anteriormente para poder guardar cada uno de ellos.
ListaCitas, listaDoctores y listaPaciente muestran el listado con la variable según escrita en el sistema cita, doc o pac.
Los métodos guardarDoctor, guardarPaciente y guardarCita están realizados a la semejanza ya que se utiliza para almacenamiento de datos.
Clase cita está conformada con cada una de las variables ya antes mencionadas para ingresar información del paciente y de qué día desea presentarse, con que doctor y etc. Con sus respectivos métodos get y set, respectivo @override.
Clase Dorctos de igual manera solo cuenta con sus respectivas variables y sus métodos get y set con su respectivo @override.
Clase Paciente de igual manera solo cuenta con las variables correspondientes y sus métodos set y get para poder ingresar los datos o mostrar los datos según sea el requerimiento del cliente.
Y por último el método mostrarMenu el cual contiene el menú a utilizar en sistema.

