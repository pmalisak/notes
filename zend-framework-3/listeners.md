# Listeners

## Redirect

    public function onSomeMethod($event)
    {
      /** @var HttpResponse $response */
      $response = $event->getResponse() ?: new HttpResponse();
      $router = $event->getRouter();
    
      $uri = $router->assemble(['yourDynamicParam' => 'sth'], ['name' => 'your-route-name']);
      $response->getHeaders()->addHeaderLine('Location', $uri);
      $response->setStatusCode(302);
    
      $event->setResponse($response);
      $event->setResult($response);
    }
