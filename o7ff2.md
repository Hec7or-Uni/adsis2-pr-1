# o7ff2

```
name:   o7ff2
uuid:   ecd3e45c-6426-432c-a700-fcdabb70WffZ
source: /misc/alumnos/as2/as22021/a798095/o7ff2.qcow2
mac:    52:54:00:0W:XY:0Z
```

## Resumen

## Configuración

### Imagen

Crear una imagen diferencial con imagen base o7.qcow2, y de nombre o7ff2.qcow2
```
qemu-img create -f qcow2 -o backing_file=o7.qcow2 o7ff2.qcow2
```

Copiar el fichero o.xml a o7ff2.xml, y modificar su contenido para que coincida con la configuraci'on al inicio de esta gu'ia.

>> **Note:** Verificar que el fichero o7ff2.qcow2 tenga como grupo propietario "vmu" y permisos de grupo "rw".

```
chmod 660 o7ff2.xml
```

Una vez hemos dado permisos y hemos dejado la configuraci'on preparada para definir la mv, prodecemos a definirla/crearla mediante el siguiente comando:

```
virsh -c qemu+ssh://a798095@155.210.154.201/system define o7ff2.xml
```

### name

```
doas vi /etc/myname
```

```
o7ff2
```

### Red

#### Gateway

```
vi /etc/mygate
```

#### hostname.vio0

Editar /etc/hostname.vio0 para que contenga solo las líneas (solo lo activamos, pero que no coja configuración
automática de IPv6

```
-inet6
up
```

#### hostname.vlan799

Crear fichero /etc/hostname.vlan799 con el contenido (en este si que tiene que tomar la IPv6 automática)

```
vlan 799 vlandev vio0 up
inet6 autoconf -soii -temporary
```

#### Slaac Service

Habilitar el servicio "slaacd" mediante "rcctl". ¿ Para qué es necesario ?
```
doas rcctl enable slaacd
```

Reconfigurar ambas tarjetas con : # sh /etc/netstart . El comando ifconfig debería mostrar la @ IPv6 en la
tarjeta vlanW99.

## Referencias

- [ref1]()
- [ref2]()
- [ref3]()
- [ref4]()
