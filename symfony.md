## Sección 1: Symfony

1. **Pregunta de Configuración:**
- Describe los pasos básicos para levantar un proyecto en Symfony.
- 1 Instalación de Symfony CLI:
    * curl -sS https://get.symfony.com/cli/installer | bash
    * Añadir ~/.symfony/bin a tu variable de entorno PATH.
  2 Crear un nuevo proyecto:
    * symfony new my_project --full
  3 Navegar al directorio del proyecto:
    * cd my_project
  4 Levantar el servidor:
    * symfony server:start
  5 Acceder a la aplicación:
    * Abrir un navegador y navegar a http://127.0.0.1:8000.

1. **Pregunta de Código:**
- Crea un controlador en Symfony que maneje una ruta /hello/{name} y devuelva un saludo personalizado. Además, si el nombre no se proporciona, debe devolver un saludo predeterminado "Hello World". (opcional) Implementa también una prueba unitaria para verificar que la ruta devuelve el saludo correcto.
- Controlador
  // src/Controller/HelloController.php
  namespace App\Controller;

  use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
  use Symfony\Component\HttpFoundation\Response;
  use Symfony\Component\Routing\Annotation\Route;

  class HelloController extends AbstractController
  {
      /**
       * @Route("/hello/{name}", name="hello", defaults={"name"="World"})
       */
      public function index(string $name): Response
      {
          return new Response(sprintf('Hello %s!', $name));
      }
  }
- prueba unitaria
    // tests/Controller/HelloControllerTest.php
    namespace App\Tests\Controller;

    use Symfony\Bundle\FrameworkBundle\Test\WebTestCase;

    class HelloControllerTest extends WebTestCase
    {
        public function testHello()
        {
            $client = static::createClient();
            $client->request('GET', '/hello/Yoan');
            $this->assertResponseIsSuccessful();
            $this->assertSelectorTextContains('body', 'Hello Yoan!');

            $client->request('GET', '/hello');
            $this->assertResponseIsSuccessful();
            $this->assertSelectorTextContains('body', 'Hello World!');
        }
    }

1. **Pregunta Teórica:**
- Explica la arquitectura de Symfony y cómo se organiza un proyecto típico en términos de carpetas y archivos.
- Carpetas y Archivos Principales:
    src/: Contiene el código fuente de la aplicación, incluidos los controladores, entidades, formularios y servicios.
    config/: Archivos de configuración del proyecto, como servicios, paquetes y rutas.
    templates/: Plantillas Twig para la vista.
    public/: Raíz pública del proyecto, contiene el archivo index.php y recursos accesibles públicamente.
    var/: Archivos temporales y de caché.
    vendor/: Dependencias del proyecto instaladas por Composer.
    bin/: Scripts ejecutables, incluido el comando de consola de Symfony.
    Arquitectura MVC:
    Modelo (Model): Representado por entidades y manejado por Doctrine ORM.
    Vista (View): Plantillas Twig que renderizan la UI.
    Controlador (Controller): Gestiona la lógica de la aplicación y las rutas.

1. **Pregunta de Código:**
- Escribe un servicio en Symfony que se inyecta en un controlador y realiza una operación matemática básica (por ejemplo, sumar dos números). ¿Qué configuraciones son necesarias para poder usarlo? (opcional) Implementa también una prueba unitaria para verificar el correcto funcionamiento del servicio.
- Servicio
    // src/Service/MathService.php
    namespace App\Service;

    class MathService
    {
        public function add(int $a, int $b): int
        {
            return $a + $b;
        }
    }

    // src/Controller/MathController.php
    namespace App\Controller;

    use App\Service\MathService;
    use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
    use Symfony\Component\HttpFoundation\Response;
    use Symfony\Component\Routing\Annotation\Route;

    class MathController extends AbstractController
    {
        private $mathService;

        public function __construct(MathService $mathService)
        {
            $this->mathService = $mathService;
        }

        /**
        * @Route("/add/{a}/{b}", name="add")
        */
        public function add(int $a, int $b): Response
        {
            $result = $this->mathService->add($a, $b);
            return new Response(sprintf('Result: %d', $result));
        }
    }
- Prueba unitaria
    // tests/Service/MathServiceTest.php
    namespace App\Tests\Service;

    use App\Service\MathService;
    use PHPUnit\Framework\TestCase;

    class MathServiceTest extends TestCase
    {
        public function testAdd()
        {
            $mathService = new MathService();
            $this->assertEquals(5, $mathService->add(2, 3));
        }
    }


1. **Pregunta de Código:**
- Muestra cómo crear un formulario en Symfony para una entidad User con campos username y email.
  - // src/Entity/User.php
    namespace App\Entity;

    use Doctrine\ORM\Mapping as ORM;

    /**
    * @ORM\Entity(repositoryClass="App\Repository\UserRepository")
    */
    class User
    {
        /**
        * @ORM\Id
        * @ORM\GeneratedValue
        * @ORM\Column(type="integer")
        */
        private $id;

        /**
        * @ORM\Column(type="string", length=100)
        */
        private $username;

        /**
        * @ORM\Column(type="string", length=100)
        */
        private $email;

        // Getters and Setters...
    }

    // src/Form/UserType.php
    namespace App\Form;

    use App\Entity\User;
    use Symfony\Component\Form\AbstractType;
    use Symfony\Component\Form\Extension\Core\Type\EmailType;
    use Symfony\Component\Form\Extension\Core\Type\TextType;
    use Symfony\Component\Form\FormBuilderInterface;
    use Symfony\Component\OptionsResolver\OptionsResolver;

    class UserType extends AbstractType
    {
        public function buildForm(FormBuilderInterface $builder, array $options)
        {
            $builder
                ->add('username', TextType::class)
                ->add('email', EmailType::class);
        }

        public function configureOptions(OptionsResolver $resolver)
        {
            $resolver->setDefaults([
                'data_class' => User::class,
            ]);
        }
    }


1. **Pregunta Teórica:**
- Explica el concepto de Dependency Injection (DI) en Symfony y cómo se configura.
    Dependency Injection (DI): Es un patrón de diseño que permite inyectar las dependencias de una clase en lugar de que la clase las cree por sí misma. En Symfony, se utiliza para gestionar la inyección de servicios en controladores, otros servicios, etc.
    Configuración en Symfony:
    Autoconfiguración y Autowiring: Symfony permite configurar los servicios automáticamente.
    services.yaml: Archivo principal de configuración de servicios.
    Inyección de Servicios: Utilizando la anotación @required o en el constructor.

1. **Pregunta de Código:**
- Escribe una consulta Doctrine en Symfony para obtener todos los registros de una entidad Product donde el precio sea mayor a 100.
    // src/Repository/ProductRepository.php
    namespace App\Repository;

    use App\Entity\Product;
    use Doctrine\Bundle\DoctrineBundle\Repository\ServiceEntityRepository;
    use Doctrine\Persistence\ManagerRegistry;

    class ProductRepository extends ServiceEntityRepository
    {
        public function __construct(ManagerRegistry $registry)
        {
            parent::__construct($registry, Product::class);
        }

        public function findExpensiveProducts(float $price): array
        {
            return $this->createQueryBuilder('p')
                        ->andWhere('p.price > :price')
                        ->setParameter('price', $price)
                        ->getQuery()
                        ->getResult();
        }
    }


1. **Pregunta Teórica:**
- ¿Qué es el Event Dispatcher en Symfony y para qué se utiliza?
    Event Dispatcher: Es un componente de Symfony que permite a los diferentes componentes de una aplicación comunicarse entre sí de manera desacoplada mediante el uso de eventos. Los eventos se disparan en varios puntos de la ejecución del código, y los listeners (o suscriptores) pueden responder a estos eventos para ejecutar lógica específica.

1. **Pregunta de Código:**
- Crea un validador personalizado en Symfony para asegurar que el campo email de una entidad User no pertenece a un dominio específico (por ejemplo, "example.com"). Muestra cómo configurar este validador y cómo sería utilizado en la entidad User.
    // src/Validator/Constraints/ForbiddenEmailDomain.php
    namespace App\Validator\Constraints;

    use Symfony\Component\Validator\Constraint;

    /**
    * @Annotation
    */
    class ForbiddenEmailDomain extends Constraint
    {
        public $message = 'The domain "{{ domain }}" is not allowed.';
    }

    // src/Validator/Constraints/ForbiddenEmailDomainValidator.php
    namespace App\Validator\Constraints;

    use Symfony\Component\Validator\Constraint;
    use Symfony\Component\Validator\ConstraintValidator;

    class ForbiddenEmailDomainValidator extends ConstraintValidator
    {
        public function validate($value, Constraint $constraint)
        {
            if (null === $value || '' === $value) {
                return;
            }

            $domain = substr(strrchr($value, "@"), 1);
            if ($domain === 'example.com') {
                $this->context->buildViolation($constraint->message)
                            ->setParameter('{{ domain }}', $domain)
                            ->addViolation();
            }
        }
    }

    // src/Entity/User.php
    namespace App\Entity;

    use App\Validator\Constraints as AppAssert;
    use Doctrine\ORM\Mapping as ORM;
    use Symfony\Component\Validator\Constraints as Assert;

    /**
    * @ORM\Entity(repositoryClass="App\Repository\UserRepository")
    */
    class User
    {
        // ...

        /**
        * @ORM\Column(type="string", length=100)
        * @Assert\Email
        * @AppAssert\ForbiddenEmailDomain
        */
        private $email;

        // ...
    }


1.  **Pregunta de Código:**
- Implementa un Event Subscriber en Symfony que escuche el evento kernel.request y registre en un archivo de log cada visita a cualquier página de la aplicación. Asegúrate de configurar el servicio correctamente para que el suscriptor se registre con el evento.
    // src/EventSubscriber/RequestLoggerSubscriber.php
    namespace App\EventSubscriber;

    use Psr\Log\LoggerInterface;
    use Symfony\Component\EventDispatcher\EventSubscriberInterface;
    use Symfony\Component\HttpKernel\Event\RequestEvent;
    use Symfony\Component\HttpKernel\KernelEvents;

    class RequestLoggerSubscriber implements EventSubscriberInterface
    {
        private $logger;

        public function __construct(LoggerInterface $logger)
        {
            $this->logger = $logger;
        }

        public function onKernelRequest(RequestEvent $event)
        {
            $request = $event->getRequest();
            $this->logger->info('New request', ['path' => $request->getPathInfo()]);
        }

        public static function getSubscribedEvents()
        {
            return [
                KernelEvents::REQUEST => 'onKernelRequest',
            ];
        }
    }

    // config/services.yaml
    services:
        App\EventSubscriber\RequestLoggerSubscriber:
            arguments:
                $logger: '@logger'
            tags:
                - { name: 'kernel.event_subscriber' }
