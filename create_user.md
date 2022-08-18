# /apiv1/user/create

## Create a new user account

### Params

-   email: string

-   bypass_activation: boolean

    -   By default, the user has to verifiy their email address before sign-in.
        With "bypass_activation" set to true, the API will be instructed to bypass required email verification step and enable automatic sign-in. What this essentially does is create a temporary password using an algorithm only known by the frontend server and the API, therefore allowing the user to automatically sign-in before initializing credentials on "welcome" page.

    -   If you are connecting directly to the API, there are a few steps needed in order to
        generate an identical password:

        -   Enable "generate_temp_password_using_secret" on your consumer
        -   Use the consumer_secret as prefix and email address as suffix for input of an SHA1 encoder
            -   Please store this secret in a secure area of the device such as Secure Enclave
        -   Generate hash

            -   GO example:

            ```
            in := consumer_secret + email
            hash := sha1.New()
            hash.Write([]byte(in))
            password := hex.EncodeToString(hash.Sum(nil))
            ```

        -   Sign-in as per usual with /apiv1/auth/issue-access-token
