import 'package:flutter/material.dart';
import 'package:hdfc_flutter_widgets/common/secondary_button.dart';
import 'package:hdfc_flutter_widgets/common/menu_button.dart';
import 'package:hdfc_flutter_widgets/event_card/common/payment_status.dart';
import 'package:hdfc_flutter_widgets/event_card/common/logo.dart';
import 'package:hdfc_flutter_widgets/event_card/common/smart_info_card.dart';
import 'package:hdfc_flutter_widgets/event_card/common/primary_detail.dart';

/// Model representing an action for the event card.
class EventCardActionItem {
  /// Action label text.
  final String title;

  /// Callback triggered on tap.
  final VoidCallback onTap;

  /// Marks the action as primary (used for button rendering logic).
  final bool isPrimary;

  EventCardActionItem({
    required this.title,
    required this.onTap,
    this.isPrimary = true,
  });
}

/// A reusable UI widget to present event or billing information in a compact, styled card.
///
/// Typically used in dashboards or transaction summaries. It shows:
/// - A header with title, subtitle, icon, and biller logo
/// - Billing/payment details
/// - Action buttons for user interaction
class CompactEventCard extends StatelessWidget {
  /// List of actions to display (at least one for primary, others as menu options).
  final List<EventCardActionItem> actionItems;

  /// SVG path of the event icon (left side).
  final String prefixIconPath;

  /// Background color behind the event icon.
  final Color prefixIconColor;

  /// SVG path of the biller logo (right side).
  final String suffixIconPath;

  /// Main title or event label.
  final String title;

  /// Optional subtitle under the title.
  final String subTitle;

  /// Smart pay status text (e.g., "Enabled", "Disabled").
  final String descriptionText;

  /// SVG icon for smart pay status.
  final String descriptionIconPath;

  /// Displayed amount (e.g., ₹ 599.00).
  final double amount;

  /// Payment status label (e.g., "Paid", "Overdue").
  final String paymentStatus;

  /// Background color of the payment status label.
  final Color paymentStatusBackgroundColor;

  /// Text/border color of the payment status label.
  final Color paymentStatusTextColor;

  /// A label string with event date and status (e.g., "12 Jan • Scheduled").
  final String eventDateWithLabel;

  /// SVG path for the menu icon (usually kebab or three dots).
  final String menuButtonIconPath;

  const CompactEventCard({
    super.key,
    required this.prefixIconPath,
    required this.suffixIconPath,
    required this.descriptionText,
    required this.descriptionIconPath,
    required this.amount,
    required this.paymentStatus,
    required this.paymentStatusBackgroundColor,
    required this.paymentStatusTextColor,
    required this.title,
    required this.prefixIconColor,
    required this.actionItems,
    required this.subTitle,
    required this.eventDateWithLabel,
    required this.menuButtonIconPath,
  });

  /// Decoration for the top section (header)
  BoxDecoration _topContainerDecoration(BuildContext context) => BoxDecoration(
        color: Colors.lightBlue[50],
        border: Border.all(color: Theme.of(context).primaryColor),
        borderRadius: const BorderRadius.only(
          topLeft: Radius.circular(20),
          topRight: Radius.circular(20),
        ),
      );

  /// Decoration for the bottom section (details + actions)
  BoxDecoration _bottomContainerDecoration(BuildContext context) => BoxDecoration(
        color: Colors.white,
        borderRadius: const BorderRadius.only(
          bottomLeft: Radius.circular(8),
          bottomRight: Radius.circular(8),
        ),
        border: Border.all(color: Theme.of(context).primaryColor),
      );

  @override
  Widget build(BuildContext context) {
    // Extract primary and secondary actions
    final EventCardActionItem? primaryAction = actionItems.isNotEmpty ? actionItems.first : null;
    final List<EventCardActionItem> secondaryActions =
        actionItems.length > 1 ? actionItems.sublist(1) : [];

    return LayoutBuilder(
      builder: (context, constraints) {
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Top section: Icon + Title + Subtitle + Status + Logo
            Container(
              decoration: _topContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 15),
              child: Row(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  // Left: Primary detail (icon, title, subtitle, status)
                  Expanded(
                    child: PrimaryDetail(
                      title: title,
                      subtitle: subTitle,
                      prefixIconPath: prefixIconPath,
                      prefixIconBackgroundColor: prefixIconColor,
                      descriptionText: descriptionText,
                      descriptionIconPath: descriptionIconPath,
                    ),
                  ),
                  // Right: Biller logo
                  Logo(svgPath: suffixIconPath, size: 50),
                ],
              ),
            ),

            // Bottom section: Amount, status, pill, buttons
            Container(
              decoration: _bottomContainerDecoration(context),
              padding: const EdgeInsets.fromLTRB(10, 15, 10, 15),
              child: Column(
                children: [
                  // Row 1: Amount + Payment Status + Date Label
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      // Left: Amount + Status
                      Expanded(
                        child: Row(
                          children: [
                            Flexible(
                              child: Text(
                                '₹ ${amount.toStringAsFixed(2)}',
                                style: const TextStyle(
                                  fontSize: 15,
                                  fontWeight: FontWeight.bold,
                                ),
                              ),
                            ),
                            const SizedBox(width: 10),
                            Flexible(
                              child: PaymentStatus(
                                status: paymentStatus,
                                borderTextColor: paymentStatusTextColor,
                                backgroundColor: paymentStatusBackgroundColor,
                              ),
                            ),
                          ],
                        ),
                      ),
                      const SizedBox(width: 2),
                      // Right: Pill label with date/status
                      Flexible(child: SmartInfoCard(text: eventDateWithLabel)),
                    ],
                  ),
                  const SizedBox(height: 10),

                  // Row 2: Primary & Secondary Actions
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      if (primaryAction != null)
                        Expanded(
                          child: SecondaryButton(
                            title: primaryAction.title,
                            onTap: primaryAction.onTap,
                          ),
                        ),
                      const SizedBox(width: 10),
                      if (secondaryActions.isNotEmpty)
                        MenuButton(
                          iconPath: menuButtonIconPath,
                          options: secondaryActions.map((e) => e.title).toList(),
                          onSelect: (selectedTitle) {
                            final selected = secondaryActions.firstWhere(
                              (item) => item.title == selectedTitle,
                            );
                            selected.onTap();
                          },
                        ),
                    ],
                  ),
                ],
              ),
            ),
          ],
        );
      },
    );
  }
}