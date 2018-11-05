# Angu6-Spring-JWT Auth
## Description des classes et principaux fonctionnements principaux de l'application BACK
* _SecurityContextHolder_ provides access to the SecurityContext
* _SecurityContext_ holds the Authentication and possibly request-specific security information
* _Authentication_ represents the principal which includes GrantedAuthority that reflects the application-wide permissions granted to a principal.
* _UserDetails contains_ necessary information to build an Authentication object from DAOs or other source of security data.
* _UserDetailsService_ helps to create a UserDetails from a String-based username and is usually used by AuthenticationProvider.
* _JwtAuthTokenFilter_ (extends OncePerRequestFilter) pre-processes HTTP request, from Token, create Authentication and populate it to SecurityContext.
* _JwtProvide_r validates, parses token String or generates token String from UserDetails.
* _UsernamePasswordAuthenticationToken_ gets username/password from login Request and combines into an instance of Authentication interface.
* _AuthenticationManager_ uses DaoAuthenticationProvider (with help of UserDetailsService & PasswordEncoder) to validate instance of UsernamePasswordAuthenticationToken, then returns a fully populated Authentication instance on successful authentication.
* _SecurityContext_ is established by calling SecurityContextHolder.getContext().setAuthentication(…​) with returned authentication object above.
* _AuthenticationEntryPoint_ handles AuthenticationException.
* Access to Restful API is protected by HTTPSecurity and authorized with Method Security Expressions.

## Base de données
Dans _ApplicationProperties_ se trouve le nom et le port de la BDD. Par défaut il s'agit de _testdb_ et du port _3306_.
Une fois l'application démarré pour la première fois il faut entrer les lignes suivantes (ne pas oublier de définir notre base par defaut) :

> INSERT INTO roles(name) VALUES('ROLE_USER')
> INSERT INTO roles(name) VALUES('ROLE_PM')
> INSERT INTO roles(name) VALUES('ROLE_ADMIN')

## Description des classes et principaux fonctionnements principaux de l'application FRONT
* _app.component_ is the parent component that contains routerLink and router-outlet for routing. It also has an authority variable as the condition for displaying items on navigation bar.
* _user.component_, _pm.component_, _admin.component_ correspond to Angular Components for User Board, PM Board, Admin Board. Each Board uses user.service to access authority data.
* _register.component_ contains User Registration form, submission of the form will call auth.service.
* _login.component_ contains User Login form, submission of the form will call auth.service and token-storage.service.
* _user.service_ gets access to authority data from Server using Angular HttpClient ($http service).
* _auth.service_ handles authentication and signup actions with Server using Angular HttpClient ($http service).
* every HTTP request by $http service will be inspected and transformed before being sent to the Server by auth-interceptor (implements HttpInterceptor).
* _auth-interceptor_ check and get Token from token-storage.service to add the Token to Authorization Header of the HTTP Requests.
* _token-storage.service_ manages Token inside Browser’s sessionStorage.

## Commande a lancé pour éviter les eventuelles erreurs de build avec le cli
_ng update --all_ 
Celà est du à une mise à jours d'angular, la commande vérifie et met automatiquement à jours nos librairies (pour uniquement une vérification 'ng update' suffit)
