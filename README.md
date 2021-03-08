# mysql_sys.session_ssl_status

SELECT 
    `sslver`.`THREAD_ID` AS `thread_id`,
    `sslver`.`VARIABLE_VALUE` AS `ssl_version`,
    `sslcip`.`VARIABLE_VALUE` AS `ssl_cipher`,
    `sslreuse`.`VARIABLE_VALUE` AS `ssl_sessions_reused`
FROM
    ((`performance_schema`.`status_by_thread` `sslver`
    LEFT JOIN `performance_schema`.`status_by_thread` `sslcip` ON (((`sslcip`.`THREAD_ID` = `sslver`.`THREAD_ID`)
        AND (`sslcip`.`VARIABLE_NAME` = 'Ssl_cipher'))))
    LEFT JOIN `performance_schema`.`status_by_thread` `sslreuse` ON (((`sslreuse`.`THREAD_ID` = `sslver`.`THREAD_ID`)
        AND (`sslreuse`.`VARIABLE_NAME` = 'Ssl_sessions_reused'))))
WHERE
    (`sslver`.`VARIABLE_NAME` = 'Ssl_version')
