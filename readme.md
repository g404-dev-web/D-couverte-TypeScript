# TP : Découverte de TypeScript

## Objectif

Apprendre les bases de TypeScript en créant une petite application de gestion de contacts.

## Prérequis

Connaissances en JavaScript, HTML et CSS.

## Étapes

### Étape 1 : Installation et configuration de TypeScript

1. Installez Node.js et npm (si ce n'est pas déjà fait) : https://nodejs.org/
2. Installez TypeScript en utilisant npm : `npm install -g typescript`
3. Créez un nouveau dossier pour le TP et initialise un projet npm : `npm init -y`
4. Installez les types pour Node.js : `npm install --save-dev @types/node`
5. Crée un fichier `tsconfig.json` pour configurer TypeScript :
   ```json
   {
     "compilerOptions": {
       "target": "es6",
       "module": "commonjs",
       "strict": true,
       "esModuleInterop": true
     },
     "include": ["src/**/*.ts"],
     "exclude": ["node_modules"]
   }
   ```

### Étape 2 : Création de l'application

1. Créez un dossier `src` et un fichier `index.ts` à l'intérieur.
2. Dans `index.ts`, définis une classe `Contact` avec les propriétés `firstName`, `lastName` et `email` :
   ```typescript
   class Contact {
     firstName: string;
     lastName: string;
     email: string;

     constructor(firstName: string, lastName: string, email: string) {
       this.firstName = firstName;
       this.lastName = lastName;
       this.email = email;
     }
   }
   ```
3. Ajoutez une méthode `fullName()` à la classe `Contact` pour retourner le nom complet du contact :
   ```typescript
   fullName(): string {
     return `${this.firstName} ${this.lastName}`;
   }
   ```
4. Créez une classe `ContactList` pour gérer un tableau de contacts :
   ```typescript
   class ContactList {
     contacts: Contact[] = [];

     addContact(contact: Contact): void {
       this.contacts.push(contact);
     }

     removeContact(contact: Contact): void {
       const index = this.contacts.indexOf(contact);
       if (index !== -1) {
         this.contacts.splice(index, 1);
       }
     }
   }
   ```
5. Ajoutez une méthode `findContacts(search: string)` à la classe `ContactList` pour rechercher des contacts par nom ou e-mail :
   ```typescript
   findContacts(search: string): Contact[] {
     return this.contacts.filter(
       (contact) =>
         contact.fullName().toLowerCase().includes(search.toLowerCase()) ||
         contact.email.toLowerCase().includes(search.toLowerCase())
     );
   }
   ```

### Étape 3 : Test de l'application

1. Dans `index.ts`, crée quelques instances de la classe `Contact` et ajoutez-les à une instance de `ContactList` :
   ```typescript
   const contactList = new ContactList();
   contactList.addContact(new Contact('John', 'Doe', 'john.doe@example.com'));
   contactList.addContact(new Contact('Jane', 'Doe', 'jane.doe@example.com'));
   ```
2. Testez la méthode `findContacts()` en recherchant des contacts par nom ou e-mail :
   ```typescript
   console.log(contactList.findContacts('Doe'));
   console.log(contactList.findContacts('john.doe@example.com'));
   ```
3. Compilez le fichier TypeScript en JavaScript en exécutant `tsc` dans le terminal.
4. Exécutez le fichier JavaScript généré avec Node.js : `node src/index.js`z
5. Vérifiez que les résultats de la recherche sont correctement affichés dans la console.

### Étape 4 : A vous de jouez

- Refactorisez le code en utilisant les modules pour avoir une seul fichier par classe ainsi qu'un fichier pour le code métier
- Intègrez l'application de gestion de contacts dans une interface utilisateur HTML/CSS.
- Ajoutez des fonctionnalités supplémentaires, comme la possibilité de modifier les contacts ou de les trier par nom grâce a des formulaire.
- Utilisez l'API JSON Placeholder pour récuperer une liste de contact