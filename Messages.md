```javascript
module.exports.messages = {
    duplicateEmailAndPhone:{
      code:'400',e
      identifier:'E_EMAIL_PHONE_EXIST',
      message:'Looks like you already have an account. Log in to continue.'
    },
    badFields: {
        code: '400',
        identifier: 'E_VALIDATION',
        message: 'Fields have not been properly populated.'
    },
    badRequest: {
        code: '400',
        identifier: 'E_BAD_REQUEST',
        message: 'Request is invalid for unspecified reasons.'
    },
    invalidCriteria: {
        code: '400',
        identifier: 'E_INVALID_CRITERIA',
        message: 'Invalid criteria passed.'
    },
    lifecycleInvalid: {
        code: '400',
        identifier: 'E_LIFECYCLE_INVALID',
        message: 'Lifecycle invalid.'
    },
    notUnique: {
        code: '400',
        identifier: 'E_NOT_UNIQUE',
        message: 'Fields require unique data.'
      },
    passwordInvalid: {
        code: '400',
        identifier: 'E_PASSWORD_INVALID',
        message: 'Password invalid.'
    },
    paymentInvalid: {
        code: '400',
        identifier: 'E_PAYMENT_INVALID',
        message: 'Payment invalid.'
    },
    purchaseInvalid: {
        code: '400',
        identifier: 'E_PURCHASE_INVALID',
        message: 'Purchase invalid.'
    },
    paymentOptionInvalid: {
        code: '400',
        identifier: 'E_PAYMENTOPTION_INVALID',
        message: 'Payment option invalid.'
    },
    unauthorized: {
        code: '401',
        identifier: 'E_PERMISSION_REQUIRED',
        message: 'Permission required.'
    },
    loginRequired: {
        code: '401',
        identifier: 'E_LOGIN_REQUIRED',
        message: 'Login required.'
    },
    forbidden: {
        code: '403',
        identifier: 'E_FORBIDDEN',
        message: 'This action is not allowed.'
      },
    notFound: {
        code: '404',
        identifier: 'E_NOT_FOUND',
        message: 'Criteria not found.'
    },
    droperatorsNotFound: {
        code: '404',
        identifier: 'E_DROPERATORS_NOT_FOUND',
        message: 'No droperators found to service area.'
    },
    userNotFound: {
        code: '404',
        identifier: 'E_USER_NOT_FOUND',
        message: 'User not found.'
    },
    emailNotFound: {
        code: '404',
        identifier: 'E_EMAIL_NOT_FOUND',
        message: 'Invalid phone number or email. Please try again.'
    },
    phoneMatchFailure: {
        code: '404',
        identifier: 'E_PHONE_NUMBER_NOT_FOUND',
        message: 'Invalid phone number or email. Please try again.'
    },
    conflict: {
        code: '409',
        identifier: 'E_CONFLICT',
        message: 'Immutable data (IDs, etc.) cannot be changed.'
    },
    immutableState: {
        code: '409',
        identifier: 'E_CONFLICT',
        message: 'State cannot be changed.'
    },
    processUnderway: {
        code: '409',
        identifier: 'E_PROCESS_UNDERWAY',
        message: 'A similar process is already active.'
    },
    deviceExists: {
        code: '409',
        identifier: 'E_DEVICE_EXISTS',
        message: 'Device already exists for this account.'
    },
    invalidStateTransition: {
        code: '409',
        identifier: 'E_CONFLICT',
        message: 'State transition is invalid.'
    },
    databaseFailed: {
        code: '500',
        identifier: 'E_DATABASE_FAILED',
        message: 'Database failed.'
    },
    notificationFailed: {
        code: '500',
        identifier: 'E_NOTIFICATION_FAILED',
        message: 'Notification failed.'
    },
    paymentFailed: {
        code: '500',
        identifier: 'E_PAYMENT_FAILED',
        message: 'Payment failed.'
    },
    serverError: {
        code: '500',
        identifier: 'E_SERVER_ERROR',
        message: 'Server has rejected this request for unspecified reasons.'
    },
    purchaseFailed: {
        code: '500',
        identifier: 'E_PURCHASE_FAILED',
        message: 'Purchase failed.'
    },
    http: {},
    emails: {},
    sockets: {},
    notifications: {
        addDevice: {
            code: 1,
            title: 'A message from DropIn',
            message: 'You have successfully signed in from new device'
        },
        operatorReserved: {
            code: 4,
            title: 'A message from DropIn',
            message: 'A gig has appeared!'
        },
        operatorClaimed: {
            code: 5,
            title: 'A message from DropIn',
            message: 'An operator has claimed your gig!'
        },
        operatorsNotFound: {
            code: null,
            title: 'A message from DropIn',
            message: 'No operators have claimed your gig :('
        },
        gigEnroute: {
            code: null,
            title: 'A message from DropIn',
            message: 'The operator is en route'
        },
        gigStarted: {
            code: 2,
            title: 'A message from DropIn',
            message: 'The gig has started'
        },
        gigFinished: {
            code: 3,
            title: 'A message from DropIn',
            message: 'The gig has finished'
        },
        docusignApproved: {
            code: 6,
            title: 'A message from DropIn',
            message: 'The gig has finished'
        }
    }
};
````
