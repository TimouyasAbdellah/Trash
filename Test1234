Si vous souhaitez éviter d'utiliser des fonctions traditionnelles avec this.skip(), vous pouvez recourir à une approche différente en utilisant une logique conditionnelle au niveau du describe ou du beforeEach pour conditionner l'exécution des tests, sans avoir à utiliser this.skip().

Voici une autre solution qui n'utilise pas de fonction traditionnelle, mais qui contourne le besoin de this.skip() en encapsulant le test dans un autre bloc conditionnel :

Exemple TypeScript sans this.skip() :

describe('Tests dépendants de l\'API', () => {
  let apiDisponible = false;

  // Vérifier la disponibilité de l'API dans le hook "before"
  before(() => {
    cy.request({
      url: 'https://api.exemple.com/health',
      failOnStatusCode: false,
    }).then((response: Cypress.Response<any>) => {
      if (response.status === 200) {
        apiDisponible = true;
      }
    });
  });

  // Vérifier la condition avant d'exécuter le bloc de tests
  if (apiDisponible) {
    describe('Exécuter les tests lorsque l\'API est disponible', () => {
      it('Test dépendant de l\'API', () => {
        cy.visit('https://votre-application.com');
        // autres actions de test ici
      });
    });
  } else {
    // Log ou autre action si l'API est indisponible
    it('API indisponible, les tests ne sont pas exécutés', () => {
      cy.log('L\'API est indisponible, tests ignorés.');
    });
  }
});

Explication :

1. Condition dans le bloc describe : La condition if (apiDisponible) est utilisée pour encapsuler l'ensemble des tests dans un autre bloc describe. Si l'API est disponible, les tests seront exécutés ; sinon, un message sera affiché, et aucun test ne sera lancé.


2. Structure claire sans this.skip() : Ici, au lieu de sauter des tests individuellement avec this.skip(), vous décidez dès le début si le bloc de tests doit être exécuté ou non.



Cela permet d'éviter l'utilisation de function() traditionnelle tout en atteignant le même objectif : conditionner l'exécution des tests en fonction de la disponibilité de l'API.

Variante plus simple :

Si vous voulez garder les choses plus simples, vous pouvez également structurer les tests directement comme ceci :

describe('Tests conditionnés par l\'API', () => {
  let apiDisponible = false;

  before(() => {
    cy.request({
      url: 'https://api.exemple.com/health',
      failOnStatusCode: false,
    }).then((response: Cypress.Response<any>) => {
      apiDisponible = response.status === 200;
    });
  });

  it('Test dépendant de l\'API', () => {
    if (!apiDisponible) {
      cy.log('L\'API est indisponible. Test ignoré.');
      return;
    }

    // Vos tests lorsque l'API est disponible
    cy.visit('https://votre-application.com');
    // autres actions de test ici
  });
});

Ici, on utilise simplement un return pour arrêter l'exécution du test si l'API est indisponible, sans utiliser this.skip().

