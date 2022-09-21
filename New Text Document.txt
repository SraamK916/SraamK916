def registration():
  username = input("Enter username or email ID: ")
  for i in range(0,len(username)):
    if ((i==0 and username[i]=='@')or(username[i]=='@' and username[i+1]=='.')or(i==0 and username[i].isdigit())or(i==0 and(username[i]=='&' or username[i]=='!'or username[i]=='%' or username[i]=='#'))):
      print('Not a valid username Please reenter valid username')
      registration()
  password = input('Enter Password ')
  digit=0
  special_char=0
  capital_letters=0
  small_letters=0
  
  for i in range(0,len(password)):
    if(password[i]=='!' or password[i]=='%' or password[i]=='#' or password[i]=='&' or password[i]=='@' ):
      special_char+=1
    if(password[i].isupper()):
      capital_letters+=1
    if(password[i].islower()):
      small_letters+=1
    if(password[i].isdigit()):
      digit+=1
  if((len(password)>5 and len(password)<16) and special_char>=1 and digit>=1 and small_letters>=1 and capital_letters>=1):
    print('Registered successfully!!!')
    db=open("login.txt", "a")
    data = username+','+password
    db.write(data)
    db.write('\n')
    db.close()
    db=open('login.txt','r')
    print(db.read())
  else:
    print('Password is not match Please try again ')
    registration()

ss="false"
i = input("Welcome to login Page.\n Enter y to create new account Enter n to LOGIN ")
if i=="y":
  registration()
if i=="n":
  user_name=input("Please enter Username/Email ID ")
  pass_word=input("Plese enter the Password ")
  db=open("login.txt","r")

  for s in db:
    a,b=s.split(",")
    b=b.strip()
    if(user_name==a and pass_word==b):
      print("Login successful!!!")
      ss='true'
      exit()
    if(user_name==a and pass_word!=b):
      print("Password is wrong.")
      l=input("Forgot Password. Enter y/n")
      if l=="y":
        print("Your password is ",b)
        ss="true"
        break
      else:
        ss="true"
        break
  if(ss=="false"):
    print("Credentials not found. Kindly register")