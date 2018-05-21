def CreateRoster(intent, session):
    dynamodb = boto3.resource('dynamodb')
    
    try:
        #try to create the table, if we fail we will fall into the `except` block
        table = dynamodb.create_table(
        TableName='HectorRoster',
        KeySchema=[
        #we are telling the database that student names will be unique (can't have two people of the same name)
            {
                'AttributeName': 'StudentName',
                'KeyType': 'HASH'
            }
        ],
        AttributeDefinitions=[
        #creating a column for students as a string and gold stars as a number
            {
                'AttributeName': 'StudentName',
                'AttributeType': 'S'
            }
        ],
        #this is just saying how fast we should read and write the data
        # default is 5, no need to go more than that
        ProvisionedThroughput={
            'ReadCapacityUnits': 5,
            'WriteCapacityUnits': 5
        }
        )
        speech_output = "Successfully created a table named Hector Roster"
    except:
        speech_output = "Table named Hector Roster already exists!"
    
    session_attributes = {}
    should_end_session =  False #change boolean when needed
    card_title = "Creating the roster!"
    reprompt_text = "Roster is available for use."
    
    return build_response(session_attributes, build_speechlet_response(
        card_title, speech_output, reprompt_text, should_end_session))
