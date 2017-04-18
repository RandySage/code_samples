cmake_minimum_required (VERSION 2.8.7)
project (INSTALL_ERROR_DEMO)

install(CODE "execute_process (
      COMMAND \"touch\" \"/dev/null/cannot/exist\"
      ERROR_VARIABLE _err
      RESULT_VARIABLE _res
)
if (NOT \${_res} EQUAL \"0\")
  message( SEND_ERROR \"err: \${_err}, res: \${_res}\")
  message( INFO \" Proceeding with any remaining steps, but 'make install' will fail\")
endif ()"
  COMPONENT compname
)

install(CODE "message( INFO \" Hypothetical later install step\")"
  COMPONENT compname
)
