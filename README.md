Osumi Framework Plugins: `OPaypal`

Este plugin añade la clase `OPaypal` al framework con la que se pueden realizar llamadas a la API de Paypal (tanto sandbox como producción).

```php
$paypal = new OPaypal(false); // true para modo sandbox y false para producción

// Indicar el código de idioma
$paypal->setLC('es');
// Indicar la moneda (EUR, USD...)
$paypal->setCurrency('EUR');
// Indicar la dirección de email usada para identificarse en Paypal
$paypal->setBusiness('user@address.com');
// Indicar URL a la que se enviará al usuario en caso de cancelar la operación
$paypal->setCancelReturn('https://www.example.com/user-cancelled');
// Indicar URL a la que se enviará al usuario en caso de operación terminada correctamente
$paypal->setOKReturn('https://www.example.com/finish-ok');
// Indicar URL de notificación para las operaciones, para llamadas "silenciosas" que se hacen desde un servidor y se recibe la respuesta más tarde de manera asíncrona
$paypal->setNotifyUrl('https://www.example.com/order-notification');
// Indicar lista de items comprados
$paypal->setItems([
  [
  'id'     => 1,
  'name'   => 'Producto 1',
  'num'    => 1,
  'amount' => 15.99
  ],
  [
  'id'     => 2,
  'name'   => 'Producto 2',
  'num'    => 1,
  'amount' => 4.5
  ],
  ...
]);
// Indicar un item individual, se puede llamar tantas veces como sea necesario
$paypal->addItem([
'id'     => 1,
'name'   => 'Producto 1',
'num'    => 1,
'amount' => 15.99
]);
// Indicar campos personalizados, sirve para realizar operaciones internas, no se notifica al usuario
$paypal->addCustom('id_order', 123);
// Obtener la URL de la llamada a Paypal con todos los datos introducidos
$url = $paypal->getRequestUrl();
// Enviar al usuario a la URL anteriormente preparada directamente
$paypal->process();
// Procesar el resultado devuelvo por la llamada a Paypal, recibe como parámetro el objeto ORequest con los datos recibidos
$paypal->processResponse($req);
```
