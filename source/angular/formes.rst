.. _formes:

================================================
Angular: formes
================================================

**Formulaires réactifs**
__________________________

Les formulaires réactifs utilisent une approche explicite et immuable pour gérer l'état d'un formulaire à un moment donné. 
Chaque modification de l'état du formulaire renvoie un nouvel état, qui maintient l'intégrité du modèle entre les modifications.

Ajout d'un contrôle de formulaire de base
-----------------------------------------

L'utilisation des contrôles de formulaire comporte trois étapes.

1. Enregistrez le module de formulaires réactifs dans votre application. Ce module déclare les directives de formulaire réactif dont vous avez besoin pour utiliser les formulaires réactifs.
2. Générez une nouvelle FormControlinstance et enregistrez-la dans le composant.
3. Enregistrez le FormControldans le modèle.

- Inscrire le module de formulaires réactifs
.. code-block::

    import { ReactiveFormsModule } from '@angular/forms';

 @NgModule({
  imports: [
    // other imports ...
    ReactiveFormsModule
  ],
 })
 export class AppModule { }
..
- Générer un nouveau FormControl
.. code-block::

    ng generate component NameEditor
..

Pour enregistrer un contrôle de formulaire unique, importez la FormControlclasse et créez une nouvelle instance 
de FormControlà enregistrer en tant que propriété de classe.
.. code-block::

    import { Component } from '@angular/core';
 import { FormControl } from '@angular/forms';

 @Component({
  selector: 'app-name-editor',
  templateUrl: './name-editor.component.html',
  styleUrls: ['./name-editor.component.css']
 })
 export class NameEditorComponent {
  name = new FormControl('');
}
..
- Enregistrer le champ dans le modèle

.. code-block::

    <label for="name">Name: </label>
 <input id="name" type="text" [formControl]="name">
..
- Afficher le composant
.. code-block::

    <app-name-editor></app-name-editor>
..
- Affichage d'une valeur de contrôle de formulaire
.. code-block::

    <p>Value: {{ name.value }}</p>
..
- Remplacement d'une valeur de contrôle de formulaire
L'exemple suivant ajoute une méthode à la classe de composant pour mettre à jour la valeur du contrôle sur Nancy 
à l'aide de la setValue()méthode.    
.. code-block::

 updateName() {
  this.name.setValue('Nancy');
 }   
..
Mettez à jour le modèle avec un bouton pour simuler une mise à jour de nom. Lorsque vous cliquez sur le bouton Mettre à jour le nom , 
la valeur entrée dans l'élément de contrôle de formulaire est reflétée comme sa valeur actuelle.    
.. code-block::

  <button (click)="updateName()">Update Name</button>
  
..
- Regroupement des champs de formulaire
Générez un ProfileEditorcomposant et importez les classes FormGroupet FormControldu @angular/formspackage.

.. code-block::

    ng generate component ProfileEditor
..
    
.. code-block::

    import { FormGroup, FormControl } from '@angular/forms';
..        
Pour ajouter un groupe de formulaires à ce composant, procédez comme suit.

1. Créez une FormGroupinstance.
2. Associez le FormGroupmodèle et la vue.
3. Enregistrez les données du formulaire.

1. Créer une instance FormGroup
Pour le formulaire de profil, ajoutez deux instances de contrôle de formulaire avec les noms firstNameet lastName.
.. code-block::

 import { Component } from '@angular/core';
 import { FormGroup, FormControl } from '@angular/forms';

 @Component({
  selector: 'app-profile-editor',
  templateUrl: './profile-editor.component.html',
  styleUrls: ['./profile-editor.component.css']
 })
 export class ProfileEditorComponent {
  profileForm = new FormGroup({
    firstName: new FormControl(''),
    lastName: new FormControl(''),
  });
 }
..   
2. Associer le modèle et la vue FormGroup
.. code-block::

 <form [formGroup]="profileForm">

  <label for="first-name">First Name: </label>
  <input id="first-name" type="text" formControlName="firstName">

  <label for="last-name">Last Name: </label>
  <input id="last-name" type="text" formControlName="lastName">

 </form>
..
3. Enregistrer les données du formulaire
.. code-block::

    <form [formGroup]="profileForm" (ngSubmit)="onSubmit()">
..
L'exemple suivant utilise console.warnpour consigner un message dans la console du navigateur.

.. code-block::

    onSubmit() {
  // TODO: Use EventEmitter with form value
  console.warn(this.profileForm.value);
 }
..
Utilisez un buttonélément pour ajouter un bouton au bas du formulaire pour déclencher la soumission du formulaire.
.. code-block::

    <p>Complete the form to enable button.</p>
 <button type="submit" [disabled]="!profileForm.valid">Submit</button>
..
- Afficher le composant
.. code-block::

    <app-profile-editor></app-profile-editor>
..

Création de groupes de formulaires imbriqués
---------------------------------------------

- Créer un groupe imbriqué
Pour créer un groupe imbriqué dans profileForm, ajoutez un addressélément imbriqué à l'instance de groupe de formulaire.
.. code-block::

 import { Component } from '@angular/core';
 import { FormGroup, FormControl } from '@angular/forms';

 @Component({
  selector: 'app-profile-editor',
  templateUrl: './profile-editor.component.html',
  styleUrls: ['./profile-editor.component.css']
 })
 export class ProfileEditorComponent {
  profileForm = new FormGroup({
    firstName: new FormControl(''),
    lastName: new FormControl(''),
    address: new FormGroup({
      street: new FormControl(''),
      city: new FormControl(''),
      state: new FormControl(''),
      zip: new FormControl('')
    })
  });
 }
..  
- Regrouper le formulaire imbriqué dans le modèle
Ajouter le addressgroupe de formulaires contenant les street, city, stateet les zipchamps au ProfileEditormodèle.
.. code-block::

    <div formGroupName="address">
  <h2>Address</h2>

  <label for="street">Street: </label>
  <input id="street" type="text" formControlName="street">

  <label for="city">City: </label>
  <input id="city" type="text" formControlName="city">

  <label for="state">State: </label>
  <input id="state" type="text" formControlName="state">

  <label for="zip">Zip Code: </label>
  <input id="zip" type="text" formControlName="zip">
 </div>
..
Création de formulaires dynamiques
----------------------------------

Pour définir un formulaire dynamique, procédez comme suit.

1. Importez la FormArrayclasse.
2. Définir un FormArraycontrôle.
3. Accédez au FormArraycontrôle avec une méthode getter.
4. Affichez le tableau de formulaires dans un modèle.


1. Importer la classe FormArray
Importez la FormArrayclasse de @angular/formsà utiliser pour les informations de type. Le FormBuilderservice est prêt à créer une FormArrayinstance.
.. code-block::

    import { FormArray } from '@angular/forms';
..
2. Définir un champ FormArray
Utilisez la FormBuilder.array()méthode pour définir le tableau et la FormBuilder.control()méthode pour remplir le tableau avec un contrôle initial.
.. code-block::

    profileForm = this.fb.group({
  firstName: ['', Validators.required],
  lastName: [''],
  address: this.fb.group({
    street: [''],
    city: [''],
    state: [''],
    zip: ['']
  }),
  aliases: this.fb.array([
    this.fb.control('')
  ])
 });
..
3. Accéder au champ FormArray
Utilisez la syntaxe getter pour créer une aliasespropriété de classe afin de récupérer le contrôle de tableau de formulaire de l'alias à partir du groupe de formulaire parent.
.. code-block::

    get aliases() {
  return this.profileForm.get('aliases') as FormArray;
 }
..
Définissez une méthode pour insérer dynamiquement un contrôle d'alias dans le tableau de formulaire de l'alias. 
La FormArray.push()méthode insère le contrôle en tant que nouvel élément dans le tableau.
.. code-block::

    addAlias() {
  this.aliases.push(this.fb.control(''));
 }
..
1. Afficher le tableau de formulaires dans le modèle
.. code-block::

    <div formArrayName="aliases">
  <h2>Aliases</h2>
  <button (click)="addAlias()" type="button">+ Add another alias</button>

  <div *ngFor="let alias of aliases.controls; let i=index">
    <!-- The repeated alias template -->
    <label for="alias-{{ i }}">Alias:</label>
    <input id="alias-{{ i }}" type="text" [formControlName]="i">
  </div>
 </div>
..
