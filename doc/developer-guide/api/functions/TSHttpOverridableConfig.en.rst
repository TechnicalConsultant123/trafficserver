.. Licensed to the Apache Software Foundation (ASF) under one
   or more contributor license agreements.  See the NOTICE file
   distributed with this work for additional information
   regarding copyright ownership.  The ASF licenses this file
   to you under the Apache License, Version 2.0 (the
   "License"); you may not use this file except in compliance
   with the License.  You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing,
   software distributed under the License is distributed on an
   "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
   KIND, either express or implied.  See the License for the
   specific language governing permissions and limitations
   under the License.

.. include:: ../../../common.defs

.. default-domain:: c

.. _ts-overridable-config:

TSHttpOverridableConfig
***************************

Synopsis
========

.. code-block:: c

    #include <ts/ts.h>

.. function:: TSReturnCode TSHttpTxnConfigIntSet(TSHttpTxn txnp, TSOverridableConfigKey key, TSMgmtInt value)
.. function:: TSReturnCode TSHttpTxnConfigIntGet(TSHttpTxn txnp, TSOverridableConfigKey key, TSMgmtInt* value)
.. function:: TSReturnCode TSHttpTxnConfigFloatSet(TSHttpTxn txnp, TSOverridableConfigKey key, TSMgmtFloat value)
.. function:: TSReturnCode TSHttpTxnConfigFloatGet(TSHttpTxn txnp, TSOverridableConfigKey key, TSMgmtFloat* value)
.. function:: TSReturnCode TSHttpTxnConfigStringSet(TSHttpTxn txnp, TSOverridableConfigKey key, const char* value, int length)
.. function:: TSReturnCode TSHttpTxnConfigStringGet(TSHttpTxn txnp, TSOverridableConfigKey key, const char** value, int* length)
.. function:: TSReturnCode TSHttpTxnConfigFind(const char* name, int length, TSOverridableConfigKey* key, TSRecordDataType* type)

Description
===========

Some of the values that are set in :file:`records.config` can be changed for a
specific transaction. It is important to note that these functions change the
configuration values stored for the transaction, which is not quite the same as
changing the actual operating values of the transaction. The critical effect is
the value must be changed before it is used by the transaction - after that,
changes will not have any effect.

All of the ``...Get`` functions store the internal value in the storage
indicated by the :arg:`value` argument. For strings :arg:`length*` will receive
the length of the string.

The values are identified by the enumeration :enum:`TSOverridableConfigKey`.
String values can be used indirectly by first passing them to
:func:`TSHttpTxnConfigFind` which, if the string matches an overridable value,
return the key and data type.

Configurations
==============

Testing :enumerator:`TS_CONFIG_BODY_FACTORY_TEMPLATE_BASE`.

The following configurations (from ``records.config``) are overridable:

========================================================================  ====================================================================
TSOverridableConfigKey Value                                              Configuration Value
========================================================================  ====================================================================
:c:enumerator:`TS_CONFIG_BODY_FACTORY_TEMPLATE_BASE`                      :ts:cv:`proxy.config.body_factory.template_base`
:c:enumerator:`TS_CONFIG_HTTP_ALLOW_HALF_OPEN`                            :ts:cv:`proxy.config.http.allow_half_open`
:c:enumerator:`TS_CONFIG_HTTP_ALLOW_MULTI_RANGE`                          :ts:cv:`proxy.config.http.allow_multi_range`
:c:enumerator:`TS_CONFIG_HTTP_ANONYMIZE_INSERT_CLIENT_IP`                 :ts:cv:`proxy.config.http.insert_client_ip`
:c:enumerator:`TS_CONFIG_HTTP_ANONYMIZE_REMOVE_CLIENT_IP`                 :ts:cv:`proxy.config.http.anonymize_remove_client_ip`
:c:enumerator:`TS_CONFIG_HTTP_ANONYMIZE_REMOVE_COOKIE`                    :ts:cv:`proxy.config.http.anonymize_remove_cookie`
:c:enumerator:`TS_CONFIG_HTTP_ANONYMIZE_REMOVE_FROM`                      :ts:cv:`proxy.config.http.anonymize_remove_from`
:c:enumerator:`TS_CONFIG_HTTP_ANONYMIZE_REMOVE_REFERER`                   :ts:cv:`proxy.config.http.anonymize_remove_referer`
:c:enumerator:`TS_CONFIG_HTTP_ANONYMIZE_REMOVE_USER_AGENT`                :ts:cv:`proxy.config.http.anonymize_remove_user_agent`
:c:enumerator:`TS_CONFIG_HTTP_ATTACH_SERVER_SESSION_TO_CLIENT`            :ts:cv:`proxy.config.http.attach_server_session_to_client`
:c:enumerator:`TS_CONFIG_HTTP_MAX_PROXY_CYCLES`                           :ts:cv:`proxy.config.http.max_proxy_cycles`
:c:enumerator:`TS_CONFIG_HTTP_AUTH_SERVER_SESSION_PRIVATE`                :ts:cv:`proxy.config.http.auth_server_session_private`
:c:enumerator:`TS_CONFIG_HTTP_BACKGROUND_FILL_ACTIVE_TIMEOUT`             :ts:cv:`proxy.config.http.background_fill_active_timeout`
:c:enumerator:`TS_CONFIG_HTTP_BACKGROUND_FILL_COMPLETED_THRESHOLD`        :ts:cv:`proxy.config.http.background_fill_completed_threshold`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_CACHE_RESPONSES_TO_COOKIES`           :ts:cv:`proxy.config.http.cache.cache_responses_to_cookies`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_CACHE_URLS_THAT_LOOK_DYNAMIC`         :ts:cv:`proxy.config.http.cache.cache_urls_that_look_dynamic`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_GENERATION`                           :ts:cv:`proxy.config.http.cache.generation`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_GUARANTEED_MAX_LIFETIME`              :ts:cv:`proxy.config.http.cache.guaranteed_max_lifetime`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_GUARANTEED_MIN_LIFETIME`              :ts:cv:`proxy.config.http.cache.guaranteed_min_lifetime`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_HEURISTIC_LM_FACTOR`                  :ts:cv:`proxy.config.http.cache.heuristic_lm_factor`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_HEURISTIC_MAX_LIFETIME`               :ts:cv:`proxy.config.http.cache.heuristic_max_lifetime`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_HEURISTIC_MIN_LIFETIME`               :ts:cv:`proxy.config.http.cache.heuristic_min_lifetime`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_HTTP`                                 :ts:cv:`proxy.config.http.cache.http`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IGNORE_ACCEPT_CHARSET_MISMATCH`       :ts:cv:`proxy.config.http.cache.ignore_accept_charset_mismatch`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IGNORE_ACCEPT_ENCODING_MISMATCH`      :ts:cv:`proxy.config.http.cache.ignore_accept_encoding_mismatch`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IGNORE_ACCEPT_LANGUAGE_MISMATCH`      :ts:cv:`proxy.config.http.cache.ignore_accept_language_mismatch`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IGNORE_ACCEPT_MISMATCH`               :ts:cv:`proxy.config.http.cache.ignore_accept_mismatch`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IGNORE_AUTHENTICATION`                :ts:cv:`proxy.config.http.cache.ignore_authentication`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IGNORE_CLIENT_CC_MAX_AGE`             :ts:cv:`proxy.config.http.cache.ignore_client_cc_max_age`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IGNORE_CLIENT_NO_CACHE`               :ts:cv:`proxy.config.http.cache.ignore_client_no_cache`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IGNORE_SERVER_NO_CACHE`               :ts:cv:`proxy.config.http.cache.ignore_server_no_cache`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_IMS_ON_CLIENT_NO_CACHE`               :ts:cv:`proxy.config.http.cache.ims_on_client_no_cache`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_MAX_OPEN_READ_RETRIES`                :ts:cv:`proxy.config.http.cache.max_open_read_retries`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_MAX_OPEN_WRITE_RETRIES`               :ts:cv:`proxy.config.http.cache.max_open_write_retries`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_MAX_STALE_AGE`                        :ts:cv:`proxy.config.http.cache.max_stale_age`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_OPEN_READ_RETRY_TIME`                 :ts:cv:`proxy.config.http.cache.open_read_retry_time`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_OPEN_WRITE_FAIL_ACTION`               :ts:cv:`proxy.config.http.cache.open_write_fail_action`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_RANGE_LOOKUP`                         :ts:cv:`proxy.config.http.cache.range.lookup`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_RANGE_WRITE`                          :ts:cv:`proxy.config.http.cache.range.write`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_REQUIRED_HEADERS`                     :ts:cv:`proxy.config.http.cache.required_headers`
:c:enumerator:`TS_CONFIG_HTTP_CACHE_WHEN_TO_REVALIDATE`                   :ts:cv:`proxy.config.http.cache.when_to_revalidate`
:c:enumerator:`TS_CONFIG_HTTP_CHUNKING_ENABLED`                           :ts:cv:`proxy.config.http.chunking_enabled`
:c:enumerator:`TS_CONFIG_HTTP_CHUNKING_SIZE`                              :ts:cv:`proxy.config.http.chunking.size`
:c:enumerator:`TS_CONFIG_HTTP_CONNECT_ATTEMPTS_MAX_RETRIES_DEAD_SERVER`   :ts:cv:`proxy.config.http.connect_attempts_max_retries_dead_server`
:c:enumerator:`TS_CONFIG_HTTP_CONNECT_ATTEMPTS_MAX_RETRIES`               :ts:cv:`proxy.config.http.connect_attempts_max_retries`
:c:enumerator:`TS_CONFIG_HTTP_CONNECT_ATTEMPTS_RR_RETRIES`                :ts:cv:`proxy.config.http.connect_attempts_rr_retries`
:c:enumerator:`TS_CONFIG_HTTP_CONNECT_ATTEMPTS_TIMEOUT`                   :ts:cv:`proxy.config.http.connect_attempts_timeout`
:c:enumerator:`TS_CONFIG_HTTP_DEFAULT_BUFFER_SIZE`                        :ts:cv:`proxy.config.http.default_buffer_size`
:c:enumerator:`TS_CONFIG_HTTP_DEFAULT_BUFFER_WATER_MARK`                  :ts:cv:`proxy.config.http.default_buffer_water_mark`
:c:enumerator:`TS_CONFIG_HTTP_DOC_IN_CACHE_SKIP_DNS`                      :ts:cv:`proxy.config.http.doc_in_cache_skip_dns`
:c:enumerator:`TS_CONFIG_HTTP_DOWN_SERVER_CACHE_TIME`                     :ts:cv:`proxy.config.http.down_server.cache_time`
:c:enumerator:`TS_CONFIG_HTTP_FLOW_CONTROL_ENABLED`                       :ts:cv:`proxy.config.http.flow_control.enabled`
:c:enumerator:`TS_CONFIG_HTTP_FLOW_CONTROL_HIGH_WATER_MARK`               :ts:cv:`proxy.config.http.flow_control.high_water`
:c:enumerator:`TS_CONFIG_HTTP_FLOW_CONTROL_LOW_WATER_MARK`                :ts:cv:`proxy.config.http.flow_control.low_water`
:c:enumerator:`TS_CONFIG_HTTP_FORWARD_CONNECT_METHOD`                     :ts:cv:`proxy.config.http.forward_connect_method`
:c:enumerator:`TS_CONFIG_HTTP_FORWARD_PROXY_AUTH_TO_PARENT`               :ts:cv:`proxy.config.http.forward.proxy_auth_to_parent`
:c:enumerator:`TS_CONFIG_HTTP_GLOBAL_USER_AGENT_HEADER`                   :ts:cv:`proxy.config.http.global_user_agent_header`
:c:enumerator:`TS_CONFIG_HTTP_INSERT_AGE_IN_RESPONSE`                     :ts:cv:`proxy.config.http.insert_age_in_response`
:c:enumerator:`TS_CONFIG_HTTP_INSERT_FORWARDED`                           :ts:cv:`proxy.config.http.insert_forwarded`
:c:enumerator:`TS_CONFIG_HTTP_INSERT_REQUEST_VIA_STR`                     :ts:cv:`proxy.config.http.insert_request_via_str`
:c:enumerator:`TS_CONFIG_HTTP_INSERT_RESPONSE_VIA_STR`                    :ts:cv:`proxy.config.http.insert_response_via_str`
:c:enumerator:`TS_CONFIG_HTTP_INSERT_SQUID_X_FORWARDED_FOR`               :ts:cv:`proxy.config.http.insert_squid_x_forwarded_for`
:c:enumerator:`TS_CONFIG_HTTP_KEEP_ALIVE_ENABLED_IN`                      :ts:cv:`proxy.config.http.keep_alive_enabled_in`
:c:enumerator:`TS_CONFIG_HTTP_KEEP_ALIVE_ENABLED_OUT`                     :ts:cv:`proxy.config.http.keep_alive_enabled_out`
:c:enumerator:`TS_CONFIG_HTTP_KEEP_ALIVE_NO_ACTIVITY_TIMEOUT_IN`          :ts:cv:`proxy.config.http.keep_alive_no_activity_timeout_in`
:c:enumerator:`TS_CONFIG_HTTP_KEEP_ALIVE_NO_ACTIVITY_TIMEOUT_OUT`         :ts:cv:`proxy.config.http.keep_alive_no_activity_timeout_out`
:c:enumerator:`TS_CONFIG_HTTP_KEEP_ALIVE_POST_OUT`                        :ts:cv:`proxy.config.http.keep_alive_post_out`
:c:enumerator:`TS_CONFIG_HTTP_NEGATIVE_CACHING_ENABLED`                   :ts:cv:`proxy.config.http.negative_caching_enabled`
:c:enumerator:`TS_CONFIG_HTTP_NEGATIVE_CACHING_LIFETIME`                  :ts:cv:`proxy.config.http.negative_caching_lifetime`
:c:enumerator:`TS_CONFIG_HTTP_NEGATIVE_REVALIDATING_ENABLED`              :ts:cv:`proxy.config.http.negative_revalidating_enabled`
:c:enumerator:`TS_CONFIG_HTTP_NEGATIVE_REVALIDATING_LIFETIME`             :ts:cv:`proxy.config.http.negative_revalidating_lifetime`
:c:enumerator:`TS_CONFIG_HTTP_NORMALIZE_AE`                               :ts:cv:`proxy.config.http.normalize_ae`
:c:enumerator:`TS_CONFIG_HTTP_NUMBER_OF_REDIRECTIONS`                     :ts:cv:`proxy.config.http.number_of_redirections`
:c:enumerator:`TS_CONFIG_HTTP_PARENT_PROXY_FAIL_THRESHOLD`                :ts:cv:`proxy.config.http.parent_proxy.fail_threshold`
:c:enumerator:`TS_CONFIG_HTTP_PARENT_PROXY_RETRY_TIME`                    :ts:cv:`proxy.config.http.parent_proxy.retry_time`
:c:enumerator:`TS_CONFIG_HTTP_PARENT_PROXY_TOTAL_CONNECT_ATTEMPTS`        :ts:cv:`proxy.config.http.parent_proxy.total_connect_attempts`
:c:enumerator:`TS_CONFIG_HTTP_PER_PARENT_CONNECT_ATTEMPTS`                :ts:cv:`proxy.config.http.parent_proxy.per_parent_connect_attempts`
:c:enumerator:`TS_CONFIG_HTTP_PER_SERVER_CONNECTION_MATCH`                :ts:cv:`proxy.config.http.per_server.connection.match`
:c:enumerator:`TS_CONFIG_HTTP_PER_SERVER_CONNECTION_MAX`                  :ts:cv:`proxy.config.http.per_server.connection.max`
:c:enumerator:`TS_CONFIG_HTTP_POST_CHECK_CONTENT_LENGTH_ENABLED`          :ts:cv:`proxy.config.http.post.check.content_length.enabled`
:c:enumerator:`TS_CONFIG_HTTP_REDIRECT_USE_ORIG_CACHE_KEY`                :ts:cv:`proxy.config.http.redirect_use_orig_cache_key`
:c:enumerator:`TS_CONFIG_HTTP_REQUEST_BUFFER_ENABLED`                     :ts:cv:`proxy.config.http.request_buffer_enabled`
:c:enumerator:`TS_CONFIG_HTTP_REQUEST_HEADER_MAX_SIZE`                    :ts:cv:`proxy.config.http.request_header_max_size`
:c:enumerator:`TS_CONFIG_HTTP_RESPONSE_HEADER_MAX_SIZE`                   :ts:cv:`proxy.config.http.response_header_max_size`
:c:enumerator:`TS_CONFIG_HTTP_RESPONSE_SERVER_ENABLED`                    :ts:cv:`proxy.config.http.response_server_enabled`
:c:enumerator:`TS_CONFIG_HTTP_RESPONSE_SERVER_STR`                        :ts:cv:`proxy.config.http.response_server_str`
:c:enumerator:`TS_CONFIG_HTTP_SEND_HTTP11_REQUESTS`                       :ts:cv:`proxy.config.http.send_http11_requests`
:c:enumerator:`TS_CONFIG_HTTP_SERVER_SESSION_SHARING_MATCH`               :ts:cv:`proxy.config.http.server_session_sharing.match`
:c:enumerator:`TS_CONFIG_HTTP_SLOW_LOG_THRESHOLD`                         :ts:cv:`proxy.config.http.slow.log.threshold`
:c:enumerator:`TS_CONFIG_HTTP_TRANSACTION_ACTIVE_TIMEOUT_IN`              :ts:cv:`proxy.config.http.transaction_active_timeout_in`
:c:enumerator:`TS_CONFIG_HTTP_TRANSACTION_ACTIVE_TIMEOUT_OUT`             :ts:cv:`proxy.config.http.transaction_active_timeout_out`
:c:enumerator:`TS_CONFIG_HTTP_TRANSACTION_NO_ACTIVITY_TIMEOUT_IN`         :ts:cv:`proxy.config.http.transaction_no_activity_timeout_in`
:c:enumerator:`TS_CONFIG_HTTP_TRANSACTION_NO_ACTIVITY_TIMEOUT_OUT`        :ts:cv:`proxy.config.http.transaction_no_activity_timeout_out`
:c:enumerator:`TS_CONFIG_HTTP_UNCACHEABLE_REQUESTS_BYPASS_PARENT`         :ts:cv:`proxy.config.http.uncacheable_requests_bypass_parent`
:c:enumerator:`TS_CONFIG_NET_SOCK_OPTION_FLAG_OUT`                        :ts:cv:`proxy.config.net.sock_option_flag_out`
:c:enumerator:`TS_CONFIG_NET_SOCK_PACKET_MARK_OUT`                        :ts:cv:`proxy.config.net.sock_packet_mark_out`
:c:enumerator:`TS_CONFIG_NET_SOCK_PACKET_TOS_OUT`                         :ts:cv:`proxy.config.net.sock_packet_tos_out`
:c:enumerator:`TS_CONFIG_NET_SOCK_RECV_BUFFER_SIZE_OUT`                   :ts:cv:`proxy.config.net.sock_recv_buffer_size_out`
:c:enumerator:`TS_CONFIG_NET_SOCK_SEND_BUFFER_SIZE_OUT`                   :ts:cv:`proxy.config.net.sock_send_buffer_size_out`
:c:enumerator:`TS_CONFIG_PARENT_FAILURES_UPDATE_HOSTDB`                   :ts:cv:`proxy.config.http.parent_proxy.mark_down_hostdb`
:c:enumerator:`TS_CONFIG_SRV_ENABLED`                                     :ts:cv:`proxy.config.srv_enabled`
:c:enumerator:`TS_CONFIG_SSL_CLIENT_CERT_FILENAME`                        :ts:cv:`proxy.config.ssl.client.cert.filename`
:c:enumerator:`TS_CONFIG_SSL_CERT_FILEPATH`                               :ts:cv:`proxy.config.ssl.client.cert.path`
:c:enumerator:`TS_CONFIG_SSL_CLIENT_VERIFY_SERVER_PROPERTIES`             :ts:cv:`proxy.config.ssl.client.verify.server.properties`
:c:enumerator:`TS_CONFIG_SSL_CLIENT_VERIFY_SERVER_POLICY`                 :ts:cv:`proxy.config.ssl.client.verify.server.policy`
:c:enumerator:`TS_CONFIG_SSL_CLIENT_SNI_POLICY`                           :ts:cv:`proxy.config.ssl.client.sni_policy`
:c:enumerator:`TS_CONFIG_SSL_HSTS_INCLUDE_SUBDOMAINS`                     :ts:cv:`proxy.config.ssl.hsts_include_subdomains`
:c:enumerator:`TS_CONFIG_SSL_HSTS_MAX_AGE`                                :ts:cv:`proxy.config.ssl.hsts_max_age`
:c:enumerator:`TS_CONFIG_URL_REMAP_PRISTINE_HOST_HDR`                     :ts:cv:`proxy.config.url_remap.pristine_host_hdr`
:c:enumerator:`TS_CONFIG_WEBSOCKET_ACTIVE_TIMEOUT`                        :ts:cv:`proxy.config.websocket.active_timeout`
:c:enumerator:`TS_CONFIG_WEBSOCKET_NO_ACTIVITY_TIMEOUT`                   :ts:cv:`proxy.config.websocket.no_activity_timeout`
:c:enumerator:`TS_CONFIG_SSL_CLIENT_CERT_FILENAME`                        :ts:cv:`proxy.config.ssl.client.cert.filename`
:c:enumerator:`TS_CONFIG_SSL_CLIENT_PRIVATE_KEY_FILENAME`                 :ts:cv:`proxy.config.ssl.client.private_key.filename`
:c:enumerator:`TS_CONFIG_SSL_CLIENT_CA_CERT_FILENAME`                     :ts:cv:`proxy.config.ssl.client.CA.cert.filename`
:c:enumerator:`TS_CONFIG_HTTP_HOST_RESOLUTION_PREFERENCE`                 :ts:cv:`proxy.config.hostdb.ip_resolve`
:c:enumerator:`TS_CONFIG_PLUGIN_VC_DEFAULT_BUFFER_INDEX`                  :ts:cv:`proxy.config.plugin.vc.default_buffer_index`
:c:enumerator:`TS_CONFIG_PLUGIN_VC_DEFAULT_BUFFER_WATER_MARK`             :ts:cv:`proxy.config.plugin.vc.default_buffer_water_mark`
========================================================================  ====================================================================

Examples
========

Enable :ref:`transaction buffer control <transaction-buffering-control>` with a
high water mark of :literal:`262144` and a low water mark of :literal:`65536`. ::

   int callback(TSCont contp, TSEvent event, void* data)
   {
      TSHttpTxn txnp = static_cast<TSHttpTxn>(data);
      TSHttpTxnConfigIntSet(txnp, TS_CONFIG_HTTP_FLOW_CONTROL_ENABLED, 1);
      TSHttpTxnConfigIntSet(txnp, TS_CONFIG_HTTP_FLOW_CONTROL_HIGH_WATER_MARK, 262144);
      TSHttpTxnConfigIntSet(txnp, TS_CONFIG_HTTP_FLOW_CONTROL_LOWER_WATER_MARK, 65536);
      return 0;
   }

See Also
========

:manpage:`TSAPI(3ts)`
