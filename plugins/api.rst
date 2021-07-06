Plugin API Reference
=====================

The following section outlines the Podrum plugin API.


.. py:class:: server()

    The Podrum server.

    .. py:attribute:: managers

        An instance of :class:`managers`.

    .. py:attribute:: rak_net_interface

        The server's raknet interface. Shouldn't be messed with.

    .. py:attribute:: logger

        The server's :class:`logger`.

    .. py:attribute:: players

        A :class:`dict` of all the players connected to the server.

    .. py:attribute:: current_entity_id

        An :class:`int`. Currently does nothing.

    .. py:attribute:: is_ticking

        A :class:`bool` that indicates whether or not the server is ticking.

    .. py:attribute:: world

        The server's default :class:`world`.
        Only available when the server is running.

    .. py:method:: get_plugin_main(name)

        Returns a plugin's main class.

        :param name: The plugin's name.
        :type name: str

        :returns: The plugin's main class, or ``None`` if not found.

    .. py:method:: get_root_path()

        Gets the path of the Podrum source.

        :returns: The path of the Podrum source.
        :rtype: :class:`str`

    .. py:method:: setup_config()

        Loads the server's configuration.

    .. py:method:: start()

        Starts the server.

    .. py:method:: dispatch_command(user_input, sender)

        Dispatches a command.

        :param user_input: The input from the user.
        :type user_input: :class:`str`

        :param sender: The person that sent the command. Can be either a player or the server.
        :type sender: Union[:class:`server`, :class:`mcbe_player`]

    .. py:method:: stop()

        Unloads all plugins, saves the world, and stops the server.

    .. py:method:: send_message(message)

        Sends a message to the console.

        :param message: The message to send.
        :type message: :class:`str`

    .. py:method:: broadcast_message(message)

        Sends a message to all online players.

        :param message: The message to broadcast.
        :type message: :class:`str`

    .. py:method:: send_chat_message(message)

        Broadcasts a message with the format ``[Server] <message>``.

        :param message: The message to send.
        :type message: :class:`str`

    .. py:method:: console_input()

        Takes input from the console and then
        dispatches a command with :func:`dispatch_command`.

    .. py:method:: find_player(username)

        Finds a player with the specified username.

        :param username: The username to search for.
        :type username: :class:`str`

        :returns: A player with the specified username, or ``None`` if not found.
        :rtype: Optional[:class:`mcbe_player`]


.. py:class:: mcbe_player(connection, server, entity_id)

    Represents a Minecraft: Bedrock Edition player.

    .. py:attribute:: connection

        The player's connection to the server.

    .. py:attribute:: server

        The :class:`server` the player is associated with.

    .. py:attribute:: world

        The :class:`world` the player is in.

    .. py:attribute:: metadata_storage

        Stores the player's metadata.

    .. py:attribute:: attributes

        A :class:`list` of the player's attributes.

    .. py:attribute:: message_format

        The format the player's messages should be sent in. Defaults to ``<%username> %message``

    .. py:attribute:: chunk_send_queue

        A :class:`Queue` for sending chunks.

    .. py:method:: chunk_send_worker()

        A worker for sending chunks.

    .. py:method:: start_chunk_send_workers(count)

        Starts a set amount of :func:`chunk_send_worker`.

        :param count: The number of workers to start.
        :type count: :class:`int`

    .. py:method:: send_start_game()

        Sends a ``start_game`` packet to the player.

    .. py:method:: send_item_component_packet()

        Sends an ``item_component`` packet to the player.

    .. py:method:: send_creative_content_packet()

        Sends a ``creative_content`` packet to the player.

    .. py:method:: send_biome_definition_list_packet()

        Sends a ``biome_definition_list`` packet to the player.

    .. py:method:: send_available_entity_identifiers_packet()

        Sends an ``available_entity_identifiers`` packet to the player.

    .. py:method:: handle_login_packet(data)

        Handles a ``login`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: disconnect(message, *, hide_disconnect_screen)

        Disconnects the player from the server.

        :param message: The message to be displayed to the player.
                        Defaults to ``Disconnected from server.``
        :type message: :class:`str`

        :param hide_disconnect_screen: Whether or not to hide the disconnect screen.
                                       Defaults to ``False``.
        :type hide_disconnect_screen: :class:`bool`

    .. py:method:: transfer(address, port)

        Transfers the player to another server.

        This disconnects the player, brings them to the main menu,
        connects them to the server.

        :param address: The address of the server to transfer the player to.
        :type address: :class:`str`

        :param port: The port of the server to transfer the player to.
                     Defaults to ``19132``.
        :type port: :class:`int`

    .. py:method:: send_form(form_id, form)

        Sends a form to the player.

        :param form_id: The ID of the form.
        :type form_id: :class:`int`

        :param form: The form to send to the player.
        :type form: :class:`form`

    .. py:method:: handle_modal_form_response_packet(data)

        Handles a ``modal_form_response`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: handle_resource_pack_client_response_packet(data)

        Handles a ``resource_pack_client_response`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: handle_packet_violation_warning_packet(data)

        Handles a ``packet_violation_warning`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: handle_request_chunk_radius_packet(data)

        Handles a ``request_chunk_radius`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: handle_move_player_packet(data)

        Handles a ``move_player`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: handle_player_action_packet(data)

        Handles a ``player_action`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: send_message(message, xuid, needs_translation)

        Sends a message to the player.

        :param message: The message to send.
        :type message: :class:`str`

        :param xuid: The XUID of the player who sent the message.
                     Defaults to an empty string.
        :type xuid: :class:`str`

        :param needs_translation: Whether or not the message needs translation.
                                  Defaults to ``False``.
        :type needs_translation: :class:`bool`

    .. py:method:: broadcast_message(message, xuid, needs_translation)

        Sends a message to all online players.

        :param message: The message to send.
        :type message: :class:`str`

        :param xuid: The XUID of the player who sent the message.
                     Defaults to an empty string.
        :type xuid: :class:`str`

        :param needs_translation: Whether or not the message needs translation.
                                  Defaults to ``False``.
        :type needs_translation: :class:`bool`

    .. py:method:: send_chat_message(message)

        Sends a message as the player.

        :param message: The message to send.
        :type message: :class:`str`

    .. py:method:: handle_text_packet(data)

        Handles a ``text`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: handle_interact_packet(data)

        Handles a ``interact`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: handle_command_request_packet(data)

        Handles a ``command_request`` packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: handle_packet(data)

        Handles an incoming packet.

        :param data: The packet's data.
        :type data: :class:`bytes`

    .. py:method:: send_chunks()

        Sends chunks to the player.

    .. py:method:: send_available_commands()

        Sends available commands to the player.

    .. py:method:: send_network_chunk_publisher_update()

        Sends a ``network_chunk_publisher_update`` packet to the player.

    .. py:method:: send_chunk(send_chunk)

        Sends a chunk to the player.

        :param send_chunk: The chunk to send.
        :type send_chunk: :class:`chunk`

    .. py:method:: send_play_status(status)

        Sends a ``play_status`` packet to the player.

        :param status: The status to send.
        :type status: :class:`int`

    .. py:method:: send_metadata()

        Sends a ``set_entity_data`` packet to the player.

    .. py:method:: send_attributes()

        Sends an ``update_attributes`` packet to the player.

    .. py:method:: send_packet(data)

        Sends a packet to the player.

        :param data: The packet's data.
        :type data: :class:`bytes`




