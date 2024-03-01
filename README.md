# Ejemplo n1

class Personaa:

    "Documentacion de la clase"

    # variable de la clase
    poblacion = []

    # metodo constructor
    def __init__(self, nombre, profesion):
        self.nombre = nombre
        self.profesion = profesion
    
    def __str__(self):
        return self.nombre

    # metodo de instancia, solo la puede llamar la instancia persona al ejecutarlo 
    def trabajo(self):
        "Documentacion del metodo"
        if self.profesion:
            mensaje = f"{self.nombre} trabaja de {self.profesion}"
        else:
            mensaje = f"{self.nombre} no esta trabajando"
        return mensaje

# la instancia persona (u objeto) de la clase Persona
persona = Personaa(nombre="Valentin", profesion="Desarrolador de Python")
print(persona.nombre, persona.profesion) # primero va el nombre del objeto y despues el metodo


# Ejemplo n2

class Poblacion:

    poblacion_total = [] # variable de clase porque esta definida en la clase, fuera de cualquier metodo de instancia y es compartida por todas las instancias creadas (almacenan datos compartidos)

    def __init__(self, ciudad, poblacion) -> None:
        self.ciudad = ciudad # variable de instancia porque tiene sus propios valores(almacenan datos especificos)
        self.poblacion = poblacion # variable de instancia porque tiene sus propios valores(almacenan datos especificos)
        Poblacion.poblacion_total.append(self) # para no hacer append en todas las instancias al ejecutarlo, va la clase Poblacion para acceder a todas

    def __str__(self) -> str: # el str sirve para el print
        return f"La ciudad {self.ciudad} tiene {self.poblacion} de habitantes"

    def __repr__(self) -> str: # representacion del objeto
        return f"Poblacion{self.ciudad}, {self.poblacion}"

    @staticmethod # metodo de clase, no lleva self (no necesito instancia, los demas def si)
    # staticmethod sirve para que no nos pida el self
    def ver_poblacion_total(): 
        for elemento in Poblacion.poblacion_total:
            print(elemento)

    
buenos_aires = Poblacion("Buenos Aires, Argentina", 4_000_000)
rosario = Poblacion("Rosario, Argentina", 3_433_232)

Poblacion.ver_poblacion_total()
        
# Ejemplo n3, herencia multiple no va el super()

class Persona:

    def __init__(self, nombre: str, apellido: str) -> None:
        self.nombre = nombre
        self.apellido = apellido

class Contacto:

    def __init__(self, celular:str) -> None:
        self.celular = celular

class Usuario(Persona, Contacto):
    
    def __init__(self, nombre: str, apellido: str, celular: str) -> None:
        # CUANDO USO HERENCIA MULTIPLE, NO ME SIRVE YA USAR EL SUPER, SINO LLAMAR A CADA CLASE EN SI
        Persona.__init__(self, nombre, apellido) # llamo a persona 
        Contacto.__init__(self, celular) # llamo a contacto
        self.contraseña = self.generar_contraseña()

    def generar_contraseña(self) -> str:
        return f"{self.nombre[:3]}{self.celular[-2:]}"

usuario = Usuario(nombre="Valentin", apellido="Cabrera", celular="3329639871") 
print(usuario.contraseña)   
