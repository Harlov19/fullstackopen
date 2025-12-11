
    endsequenceDiagram
    actor User
    participant UI as Login Page (UI)
    participant AuthC as AuthController
    participant AuthS as AuthService
    participant DB as User Database
    participant Token as JWT Service
    participant Redirect as Role-Based Redirector

    User ->> UI: Open login page
    User ->> UI: Enter username & password
    UI ->> AuthC: Submit login form
    AuthC ->> AuthS: validateCredentials(username, password)

    AuthS ->> DB: queryUser(username)
    DB -->> AuthS: userRecord / null

    alt User exists
        AuthS ->> AuthS: verifyPassword()
        alt Password correct
            AuthS ->> Token: generateJWT(userId, role)
            Token -->> AuthS: jwtToken
            AuthS -->> AuthC: authenticationSuccess(jwtToken, role)
            AuthC ->> Redirect: redirectUser(role)

            alt Admin Role
                Redirect -->> UI: Load Admin Dashboard
            else Doctor Role
                Redirect -->> UI: Load Doctor Dashboard
            else Patient Role
                Redirect -->> UI: Load Patient Dashboard
            end

        else Password incorrect
            AuthS -->> AuthC: authenticationFailed("Invalid credentials")
            AuthC -->> UI: Show error: "Incorrect email or password"
        end

    else User not found
        AuthS -->> AuthC: authenticationFailed("Invalid credentials")
        AuthC -->> UI: Show error message
    end

    %% Forgot Password Extension
    opt Forgot Password (E1)
        User ->> UI: Click "Forgot Password"
        UI ->> AuthC: initiatePasswordReset()
        AuthC ->> AuthS: sendResetLink()
        AuthS ->> User: Email reset link
    end

    %% Remember Me Extension
    opt Remember Me (E2)
        UI ->> AuthC: Request extended session
        AuthC ->> Token: generateLongLivedToken()
        Token -->> UI: Store long-lived session token
    end

    %% Exception Handling
    opt Database Error
        AuthS ->> DB: queryUser()
        DB -->> AuthS: Error (Connection issue)
        AuthS -->> AuthC: authenticationFailed("System Error")
        AuthC -->> UI: Show "System temporarily unavailable"
