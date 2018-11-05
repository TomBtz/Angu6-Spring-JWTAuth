# Angu6-Spring-JWT Auth
## Description des class et fonctionnement principaux de l'application back
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
