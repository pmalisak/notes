## Konfiguracja

    suites:
      foo:
        paths:
          - %paths.base%/test/features/
        contexts:
          - Test\ContextFirst
          - Test\ContextSecond
      bar:
        paths:
          - %paths.base%/test/features2/
        contexts:
          - Test\ContextBar

`ContextFirst` oraz `ContextSecond` dzielą ze sobą metody scenariuszowe. Natomiast `ContextBar` jest już w osobnym suite więc nie ma dostępu do pozostałych klas kontekstowych.

Metody scenariuszowe w kontekście pojedynczego suite muszą być unikalne.
