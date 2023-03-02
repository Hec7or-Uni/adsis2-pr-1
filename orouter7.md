# orouter1

```
name:   orouter7
uuid:   ecd3e45c-6426-432c-a700-fcdabb70WffZ
source: /misc/alumnos/as2/as22021/a798095/orouter7.qcow2
mac:    52:54:00:0W:XY:0Z
```

## Resumen


## Configuraci'on

### Imagen

Crear una imagen diferencial con imagen base o7.qcow2, y de nombre orouter7.qcow2
```
qemu-img create -f qcow2 -o backing_file=o7.qcow2 orouter7.qcow2
```

Copiar el fichero o.xml a orouter7.xml, y modificar su contenido para que coincida con la configuraci'on al inicio de esta gu'ia.

>> **Note:** Verificar que el fichero orouter7.qcow2 tenga como grupo propietario "vmu" y permisos de grupo "rw".

```
chmod 660 orouter7.xml
```

Una vez hemos dado permisos y hemos dejado la configuraci'on preparada para definir la mv, prodecemos a definirla/crearla mediante el siguiente comando:

```
virsh -c qemu+ssh://a798095@155.210.154.201/system define orouter7.xml
```

## Nombre

Modificamos el nombre de la maquina:

```
doas vi /etc/myname
```

```
orouter7
```

### Red

#### Red Exterior

Modifica el fichero `/etc/hostname.vio0` para que funcione sólo con la @ `2001:470:736b:f000::171` 

```
```

A continuaci'on modificamos el fichero `/etc/mygate` para que solo incluya el encaminador IPv6 principal por defecto de su subred es decir, el router "central"

```
```

#### Red Interna

Copiar fichero `/etc/hostname.vio0` a otro con nombre `/etc/hostname.vlanW99`. Modificar, este último, para
poner @IPv6=`2001:470:736b:WXY::1` y la vlan =W99, indicando como dispositivo asociado vio0

```
```

---

Para activar encaminamiento ip6 y no contestación a anuncios de prefijo ip6, modificar `/etc/sysctl.conf`.

```
cp /etc/examples/sysctl.conf /etc/sysctl.conf
doas vi /etc/sysctl.conf
```

```
net.inet6.ip6.forwarding=1
```

Hay que poner en funcionamiento el servicio de anuncio de prefijos IPv6 a la subred de la vlan

Poner en marcha el servicio rad (mirar páginas man en internet), mediante activación de servicio, en
/etc/rc.conf.local, incluyendo rad_flags="" o mediante comando rcctl (mirar paginas man en internet).
Adicionalmente, indicar la tarjeta, en la que se anuncia la información de prefijo y encaminador por defecto,
en el fichero "/etc/rad.conf" con la nueva línea "interface <vuestro_interface>". Se pueden precisar aspecto
adicionales de funcionamiento de este servicio en este fichero de configuración, pero, por ahora, no son
necesarios

### Paso 2

## Referencias

- [ref1]()
- [ref2]()
- [ref3]()
- [ref4]()
