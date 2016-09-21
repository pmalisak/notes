# Listeners

## Redirect

    public function onSomeMethod($event)
    {
      /** @var \Zend\Http\Response $response */
      $response = $event->getResponse() ?: new \Zend\Http\Response();
      $router = $event->getRouter();
    
      $uri = $router->assemble(['yourDynamicParam' => 'sth'], ['name' => 'your-route-name']);
      $response->getHeaders()->addHeaderLine('Location', $uri);
      $response->setStatusCode(302);
    
      $event->setResponse($response);
      $event->setResult($response);
    }

## Get param from route

    public function onSomeMethod($event)
    {
        if (! $matches = $event->getRouteMatch()) {
            return null; // not found in route => 404
        }

        $params = $matches->getParams();
        $controllerName = isset($params['controller']) ? $params['controller'] : null;
    }
